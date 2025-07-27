# QM/MM_Gromacs
Практикум по QM/MM молекулярной динамике и метадинамике
> *Цель практикума ознакомиться с возможностями и отличиями QM/MM MD*

## Установка singularity и gromacs-dftb+
- Будем использовать интерфейс gromacs-dftb+. Воспользуемся готовым контейнером.
```bash
# установим singularity
wget https://github.com/sylabs/singularity/releases/download/v3.11.5/singularity-ce_3.11.5-jammy_amd64.deb
sudo dpkg -i singularity-ce_3.11.5-jammy_amd64.deb
sudo apt install -f
```
```bash
# зададим alias
alias gmx='singularity run -B $(pwd) --nv /path/to/sif_file'
```
## Перенос протона в малоновом альдегиде
- Создадим бокс с альдегидом и добавим воду
```
gmx editconf -f mal -o box -d 0.7 -bt cubic
gmx solvate -cp box -cs -o solv -p mal
```
