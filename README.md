# QM/MM_Gromacs
Практикум по QM/MM молекулярной динамике и метадинамике
> *Цель практикума ознакомиться с возможностями и отличиями QM/MM MD*

## Установка singularity и gromacs-dftb+
- Будем использовать интерфейс gromacs-dftb+. Воспользуемся готовым контейнером.
```
# установим singularity
wget https://github.com/sylabs/singularity/releases/download/v3.11.5/singularity-ce_3.11.5-jammy_amd64.deb
sudo dpkg -i singularity-ce_3.11.5-jammy_amd64.deb
sudo apt install -f
```
```
# зададим alias
alias gmx='singularity run -B $(pwd) --nv /path/to/sif_file'
```
