# Witness deployment from binaries HF22
This are the files and steps needed to instal wekud HardFork22

Step by step for dummies, only for UBUNTU 16.04

This tutorial assumes you know how to login remotely to your server using shh or whatever you prefer, if that is not the case, maybe you don't have bare minimum knowledge pre-requirements to run a witness node.



#### First steps: 
Install git, screen and nano editor, move to home folder, clone repository (download)
```

sudo apt-get install git nano screen

cd ~

git clone https://github.com/nnnarvaez/weku_hf22/ 

```

**NOTE:** You might need other dependencies an C++ libraries, if after following this instructions your wekud or cli_walletHF22 result in an error please [try this](https://github.com/nnnarvaez/weku_hf22/dependencies.md)


#### Edit config file
Add your witness name and private WIF
Once added press: `<CTRL-X> <Y> <ENTER>`
control X requests to exit, it will ask if you want to save the changes, the Y tells it that yes you want, and asks for a filename, you press enter to overwrite the original `config.ini`

```
cd weku_hf22

nano ./witness_node_data_dir/config.ini

```

#### Optional: Optimize linux swap management to speed replays
For the daring and dangerous.
```
echo    75 | sudo tee /proc/sys/vm/dirty_background_ratio &&
echo  1000 | sudo tee /proc/sys/vm/dirty_expire_centisecs &&
echo    80 | sudo tee /proc/sys/vm/dirty_ratio &&
echo 30000 | sudo tee /proc/sys/vm/dirty_writeback_centisecs
``` 

#### Run the WEKU daemon 
This step will take long time (many hours) you can press `<CTRL> <A> <D>` to send the screen to the background, but it is better if you monitor it in case there are problems

```
sudo screen -dmS WEKU-witness
sudo screen -r WEKU-witness
./wekud
```

#### Recovering the screen from the backgroud to monitor WEKU daemon

```
sudo screen -r WEKU-witness
```` 

To exit again press: `<CTRL> <A> <D>`

#### If you did the optional step about linux swap management
Revert to default values once your replay is done. 

```
echo    10 | sudo tee /proc/sys/vm/dirty_background_ratio &&
sudo rm -fr /proc/sys/vm/dirty_expire_centisecs &&
echo    20 | sudo tee /proc/sys/vm/dirty_ratio &&
sudo rm -fr /proc/sys/vm/dirty_writeback_centisecs 
```
