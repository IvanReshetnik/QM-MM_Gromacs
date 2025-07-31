# QM/MM_Gromacs
> *Цель практикума ознакомиться с возможностями и отличиями QM/MM MD*

## Установка singularity и gromacs-dftb+
- Будем использовать интерфейс gromacs-dftb+. Воспользуемся готовым контейнером.
```
# установим singularity
wget https://github.com/sylabs/singularity/releases/download/v3.11.5/singularity-ce_3.11.5-jammy_amd64.deb
sudo dpkg -i singularity-ce_3.11.5-jammy_amd64.deb
sudo apt install -f
```
```bash
# зададим alias
alias gmx='singularity exec -B $(pwd) --nv /path/to/sif_file /usr/local/gromacs/bin/gmx'
```
## Перенос протона в малоновом альдегиде
- Создадим бокс с альдегидом и добавим воду
```
gmx editconf -f ./md_files/mal -o box -d 0.7 -bt cubic
gmx solvate -cp box -cs -o solv -p ./md_files/mal
```
- Минимизируем энергию
```
gmx grompp -f ./md_files/em.mdp -c solv -p ./md_files/mal.top -o em -maxwarn 1
```
- Уравновесим систему
```
gmx grompp -f ./md-files/nvt.mdp -c em -r em -p ./md-files/mal -o nvt
gmx mdrun -v -deffnm nvt
gmx grompp -f ./md-files/npt.mdp -c nvt -r nvt -t nvt -p mal -o npt
gmx mdrun -v -deffnm npt
```
- Запустим симуляцию MD
```
gmx grompp -f qmmm.mdp -c npt -p mal -o qmmm -maxwarn 1
gmx mdrun -v -deffnm qmmm
```

