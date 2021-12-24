# PubHunt - Hunt for Puzzles Public keys
![alt text](https://raw.githubusercontent.com/phrutis/LostCoins/main/Others/puzzle.jpg "PubHunt")
</br>forked from [PubHunt](https://github.com/kanhavishva/PubHunt)</br>

## It searches for random compressed Public keys for given hash160.

## The idea to do this
This is only useful for Bitcoin [puzzle transaction](https://www.blockchain.com/btc/tx/08389f34c98c606322740c0be6a7125d9860bb8d5cb182c02f98461e5fa6cd15).</br>
For the [puzzles](https://privatekeys.pw/puzzles/bitcoin-puzzle-tx) **64, 66, 67, 68, 69, 71** or **72** and some more... </br>
There are no Public keys are available, so if we can able to find Public keys for those addresses. </br>
Then [Collider](https://github.com/phrutis/Collider) algorithm can be used to solve those puzzles.</br>
That's it, cheers 🍺 

## How does it work
A public key is randomly generated and compared with the hash160 of the [puzzle](https://privatekeys.pw/puzzles/bitcoin-puzzle-tx) address.</br>
Random Public key -> Rimpd160 from address

## According to theory 
1 puzzle address(ripemd160) is equal to **79,228,162,514,264,337,593,543,950,336** private keys in 256 bit</br> 
**79,228,162,514,264,337,593,543,950,336** private keys = **79,228,162,514,264,337,593,543,950,336** public keys</br>
**79,228,162,514,264,337,593,543,950,336** public keys = **1** puzzle address</br>
Therefore, the chance of finding an address collision is much higher. &#127870; &#x20BF;

## Usage
This is GPU only, no CPU support. 

```
PubHunt.exe -h
PubHunt [-check] [-h] [-v]
        [-gi GPU ids: 0,1...] [-gx gridsize: g0x,g0y,g1x,g1y, ...]
        [-o outputfile] [inputFile]

 -v                       : Print version
 -gi gpuId1,gpuId2,...    : List of GPU(s) to use, default is 0
 -gx g1x,g1y,g2x,g2y, ... : Specify GPU(s) kernel gridsize, default is 8*(MP number),128
 -o outputfile            : Output results to the specified file
 -l                       : List cuda enabled devices
 -check                   : Check CPU and GPU kernel vs CPU
 inputFile                : List of the hash160, one per line in hex format (text mode)
```

- Run: ```PubHunt.exe -gi 0 -gx 9216,1024 hashP64.txt```
- Run: ```PubHunt.exe -gi 0 -gx 8192,1024 hashP64.txt```

```
C:\Users\BOSS>PubHunt.exe -gi 0 -gx 9216,1024 hashP64.txt

PubHunt v1.00 (24.12.2021 phrutis Edition)

DEVICE       : GPU
GPU IDS      : 0
GPU GRIDSIZE : 9216x1024
NUM HASH160  : 1
OUTPUT FILE  : Found.txt
GPU          : GPU #0 NVIDIA GeForce RTX 2070 (36x64 cores) Grid(9216x1024)

[00:10:37] [GPU: 363.60 Gkeys/s] [T: 242,432,650,248,192] [F: 0]
```

## Building
##### Windows
- Microsoft Visual Studio Community 2019 
- CUDA version [10.22](https://developer.nvidia.com/cuda-10.2-download-archive?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exenetwork)
##### Linux
 - Edit the makefile and set up the appropriate CUDA SDK and compiler paths for nvcc. Or pass them as variables to `make` command.

    ```make
    CUDA       = /usr/local/cuda-11.5
    CXXCUDA    = /usr/bin/g++
    ```
 - To build CPU-only version (without CUDA support):
    ```sh
    $ make all
    ```
 - To build with CUDA:
    ```sh
    $ make gpu=1 CCAP=35 all
    ```
## License
PubHunt is licensed under GPLv3.

## Disclaimer
ALL THE CODES, PROGRAM AND INFORMATION ARE FOR EDUCATIONAL PURPOSES ONLY. USE IT AT YOUR OWN RISK. THE DEVELOPER WILL NOT BE RESPONSIBLE FOR ANY LOSS, DAMAGE OR CLAIM ARISING FROM USING THIS PROGRAM.

