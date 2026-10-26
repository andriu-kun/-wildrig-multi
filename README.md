# WildRig Multi
multi algo miner for AMD, NVIDIA and Intel gpu's

[Discord community](https://discord.gg/ZGDaQ6edXb)

# KNOWN ISSUES
- **nexapow** is not supported on AMD gpu's with pre-RDNA architecture
- **evohash** and some other x-like algorithms produce incorrect shares on NVIDIA Blackwell gpu's
- any report is welcome! :)

# SUPPORTED GPU's
## AMD:
- **GCN 2nd gen**: Radeon R7 260, R9 290, R9 295X2, R7 360, R9 390
- **GCN 3rd gen**: Radeon R9 285, R9 380, R9 Fury, R9 Nano
- **GCN 4th gen**: Radeon RX 460, 470, 480, 550, 560, 570, 580, 590
- **GCN 5th gen**: Radeon Vega 56, Vega 64, Vega FE, Radeon VII
- **RDNA 1st gen**: Radeon RX 5500, 5600, 5700
- **RDNA 2nd gen**: Radeon RX 6500, 6600, 6700, 6750, 6800, 6900, 6950
- **RDNA 3rd gen**: Radeon RX 7600, 7700, 7800, 7900
- **RDNA 4th gen**: Radeon RX 9070

Pitcairn, Tahiti and other old cards of **GCN 1st gen**(like HD 78x0, HD 79x0, R7 265, R9 270, R9 280, R9 370, etc.) are not supported and won't be, because they are too old and need additional work.

## NVIDIA:
- **Maxwell**: GTX 750, GTX 9x0 series, Titan X, Tesla M-series
- **Pascal**: GTX 10x0 series, Titan Xp, Tesla P-series, P106-090, P106-100, P104-100, P104-101, P102-100, P102-101
- **Volta**: Tesla V-series, CMP 100HX-210
- **Turing**: GTX 16x0 series, RTX 20x0 series, Tesla T-series, Quadro Turing, CMP 30HX, CMP 40HX, CMP 50HX
- **Ampere**: RTX 30x0 series, Quadro Ampere, CMP 70HX, CMP 90HX, CMP 170HX
- **Ada Lovelace**: RTX 40x0 series, Quadro Ada
- **Blackwell**: RTX 50x0 series

Minimum driver versio is 452.39+ on Windows and 450.80.02+ on Linux. Supported list of gpu's is much longer, but not all of them have default intensity value, so use parameter *--gpu-instensity* to get better hashrate

## INTEL:
- **Intel Arc Alchemist**: A310(E), A350(M,E), A370(M,E), A380(E), A530M, A550M, A570M, A580(E), A730M, A750(E), A770(M)
- **Intel Arc Alchemist Pro**: A30M, A40/A50, A60M, A60
- **Intel Arc Battlemage**: B570, B580
- **Intel Data Center GPU**: Flex 140, Flex 170

# SUPPORTED ALGORITHMS
- anime
- bitcore, blake2s, bmw512
- c11, curvehash
- evrprogpow
- firopow
- ghostrider
- heavyhash, hex, hmq1725
- kawpow
- lyra2v2
- megabtx, memehash, meowpow
- nexapow, nist5
- pearlhash, phi, progpowz, progpow-sero, progpow-telestai
- qhash, quark, qubit
- sha256, sha256csm, sha256d, sha256q, sha256t, sha512256d, shandwich256, skein2, skunkhash, skydoge
- timetravel, tribus
- x11, x11k, x12, x13, x14, x15, x16r, x16rv2, x16rt, x16s, x17, x18, x20r, x21s, x22i, x25x, x33

# DEV-FEE:

All algorithms are zero fee except listed below.

- **0.75%**:
  - evrprogpow
  - firopow
  - kawpow
  - meowpow
  - nexapow
  - progpow-quai
  - progpow-sero
  - progpow-telestai
  - progpowz
- **1.00%**:
  - curvehash
  - ghostrider
  - mike
- **2.00%**:
  - skydoge
  - qhash

# OPTIONS
```
Usage: wildrig [OPTIONS]

  Some parameters can be set per gpu, use comma to separate each gpu and * to skip

Options:
  -a, --algo ALGO               specify the hash algorithm to use
      --benchmark                run offline benchmark
      --benchmark-hashorder      run offline benchmark and/or set hash order for benchmark
      --benchmark-epoch          run offline benchmark and/or set epoch for benchmark
      --benchmark-block          run offline benchmark and/or set block for benchmark
      --benchmark-timeout        run offline benchmark and/or set how long to run benchmark in seconds(default: 0)

  -o, --url URL                  URL of mining server
      --proxy                    set ip:port to connect via SOCKS5 proxy
  -O, --userpass U:P             username:password pair for mining server
  -u, --user USERNAME            username for mining server
  -p, --pass PASSWORD            password for mining server
  -w, --worker WORKERNAME        worker name(progpow variants only)
  -r, --retries N                number of times to retry before switch to backup server (default: 1)
  -R, --retry-pause N            time to pause between retries (default: 5)
      --max-rejects N            number of one by one rejects before switch to backup server (default: 5)
      --max-difficulty N         maximum difficulty to accept from pool(unit: M), otherwise reconnect (default: 0)

      --send-stale               send stale shares
      --diff-factor N            difficulty factor to use instead of algo default(default: 0)
      --no-extranonce            disable exranonce subscription
      --protocol PROTOCOL        set stratum protocol(ethproxy, ethstratum, stratum, stratum1, stratum2)

      --watchdog                 enable checking how long videocards are running OpenCL kernel(terminate if more than 30 sec.)
      --watchdog-script FILE     file to execute when watchdog triggers(can be used without --watchdog parameter)
      --strategy N               strategy of feeding videocards with job(default: 0)
      --split-job N              amount of gpu's(or threads of it, keep this in mind) solving one job

      --opencl-platforms LIST    list of OpenCL platforms to use(amd, nvidia or intel; default: all)
      --force-eff-mode           force to use efficient kernels when possible(e.g. memehash, skydoge)
      --progpow-kernel           depends on drivers values 1 or 2 can provide better hashrate for ProgPow(default: 0)
      --no-dag-split             disable splitting DAG on two parts(have sense only if AMD fix this problem in their drivers)
      --print-platforms          print available OpenCL platforms and exit
      --print-devices            print available OpenCL devices and exit

      --no-adl                   disable monitoring via ADL
      --no-igcl                  disable monitoring via IGCL
      --no-nvml                  disable monitoring via NVML
      --no-sysfs                 disable monitoring via sysfs

  -d, --gpu-list LIST            list of gpu's to use(default: all)
      --gpu-threads N            set amount of threads per gpu(default: auto)
      --gpu-affinity N           affine GPU threads to a specific CPU thread
  -i, --gpu-intensity N          set intensity per gpu(default: auto)

      --gpu-temp-limit N         set temperature at which gpu will stop mining(default: 85)
      --gpu-temp-resume N        set temperature at which gpu will resume mining(default: 60)

      --gpu-reset-oc             reset gpu overclock settings on start
      --gpu-delay-oc N           delay gpu overclock settings in seconds(default: 0)
      --gpu-core-clock N         lock GPU core clock to N
      --gpu-core-offset N        set offset N for GPU core clock
      --gpu-memory-clock N       lock GPU memory clock to N
      --gpu-memory-offset N      set offset N for GPU memory clock
      --gpu-powerlimit N         set power limit for GPU to N
      --gpu-fan-speed N          set fan speed for GPU to N

      --execute-at-start FILE    execute custom script before gpu initialization
      --execute FILE             execute custom script after gpu initialization or precompute stage, etc.
      --execute-wait N           wait for N seconds after executing the script (default: 1)

      --multiple-instance        allow multiple instances running at one time
  -l, --log-file FILE            log all output to a file

      --no-color                 disable colored output
      --print-time N             print hashrate report every N seconds
      --print-debug              print debug information

      --api-port N               port for API
      --api-worker-id ID         custom worker-id for API

  -h, --help                     display this help and exit
  -V, --version                  output version information and exit
```

# LICENSE
```
THIS SOFTWARE IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED,
INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A
PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS BE LIABLE
FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR
OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.
```
