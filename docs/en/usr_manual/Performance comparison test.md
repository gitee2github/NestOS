# Performance comparison test

Compare openEuler21.09, openEuler20.03LTS, and Centos8 operating docker,podman, and iSulad container engine performance using NestOS beta. The test results are as follows. The parameters of the x86_64 and aarch64 VMS are as follows:

| Configuration | Information  |
| :-----------: | :----------: |
|      OS       |    NestOS、openEuler21.09、openEuler20.03LTS、CentOS8    |
|    CPU  | 8 cores |
|    Memory     |                        8 GB                        |

Software Version:

| Name   | Version                                                      |
| ------ | ------------------------------------------------------------ |
| iSulad | Version 2.0.10                                               |
| docker | Version: 18.09.0                                             |
| podman | openEuler：Version 0.10.1<br/>NestOS：Version 3.1.0<br/>CentOS8：Version 3.3.1 |

Docker(x86_64) test results:

| operator(ms) | NestOS | openEuler21.09 | openEuler20.03LTS | CentOS8 | vs openEuler21.09 | vs openEuler20.03LTS | vs CentOS8 |
| :----------: | :----: | :----: | :----: | :-------: | :-------: | :-------: | :-------: |
|  100*creat   |  2167  |      2302      |  10007  |   5406   |   -6%    |   -79%   |   -60%   |
|  100*start   |  11742  |  17596  |       19238       |  12450  |   -34%   |   -39%   |   -6%   |
|   100*stop   |  1713  |  11501  |  11126  |   2436   |   -86%   |   -85%   |   -30%   |
|    100*rm    |  1733  |  1892  |  2057  |   3191   |   -9%    |   -16%   |   -46%   |

Docker(aarch64)test results：

| operator(ms) | NestOS | openEuler21.09 | openEuler20.03LTS | CentOS8 | vs openEuler21.09 | vs openEuler20.03LTS | vs CentOS8 |
| :----------: | :----: | :------------: | :---------------: | :-----: | :---------------: | :------------------: | :--------: |
|  100*creat   |  1967  |      2368      |       2703        |  9430   |       -20%        |         -37%         |   -379%    |
|  100*start   |  6529  |      7945      |       7109        |  11074  |       -21%        |         -9%          |    -45%    |
|   100*stop   |  1184  |     11209      |       11033       |  4435   |       -846%       |        -831%         |    -74%    |
|    100*rm    |  1379  |      1645      |       1659        |  5511   |       -17%        |         -17%         |    -75%    |

iSulad(x86_64)test results：

| operator(ms) | NestOS | openEuler21.09 | openEuler20.03LTS | CentOS8 | vs openEuler21.09 | vs openEuler20.03LTS | vs CentOS8 |
| :----------: | :----: | :------------: | :---------------: | :-----: | :---------------: | :------------------: | :--------: |
|  100*creat   |  817   |      1083      |       3693        |  1340   |       -25%        |         -78%         |    -40%    |
|  100*start   |  1822  |      2256      |       5947        |  3524   |       -20%        |         -70%         |    -49%    |
|   100*stop   |  328   |      507       |       1180        |   584   |       -36%        |         -73%         |    -44%    |
|    100*rm    |  839   |      896       |       1272        |  1023   |        -7%        |         -35%         |    -18%    |

iSulad(aarch64)test results：

| operator(ms) | NestOS | openEuler21.09 | openEuler20.03LTS | CentOS8 | vs openEuler21.09 | vs openEuler20.03LTS | vs CentOS8 |
| :----------: | :----: | :------------: | :---------------: | :-----: | :---------------: | :------------------: | :--------: |
|  100*creat   |  558   |      614       |       1181        |  1077   |       -10%        |         -53%         |    -49%    |
|  100*start   |  1883  |      2019      |       2927        |  2310   |        -7%        |         -36%         |    -19%    |
|   100*stop   |  268   |      334       |        388        |  2555   |       -20%        |         -31%         |   -853%    |
|    100*rm    |  428   |      547       |        555        |   694   |       -22%        |         -23%         |    -39%    |

Podman(x86_64)test results：

| operator(ms) | NestOS | openEuler21.09 | openEuler20.03LTS | CentOS8 | vs openEuler21.09 | vs openEuler20.03LTS | vs CentOS8 |
| :----------: | :----: | :------------: | :---------------: | :-----: | :---------------: | :------------------: | :--------: |
|  100*creat   |  5892  |     24383      |       21040       |  11535  |       -313%       |        -257%         |    -96%    |
|  100*start   |  8560  |     14086      |       11997       |  16141  |       -65%        |         -40%         |    -89%    |
|   100*stop   |  5942  |      1982      |       1658        |  2472   |       +66%        |         +72%         |    +58%    |
|    100*rm    |  6886  |     11756      |       12209       |  3221   |       -71%        |         -77%         |    +53%    |

Podman(aarch64)test results：

| operator(ms) | NestOS | openEuler21.09 | openEuler20.03LTS | CentOS8 | vs openEuler21.09 | vs openEuler20.03LTS | vs CentOS8 |
| :----------: | :----: | :------------: | :---------------: | :-----: | :---------------: | :------------------: | :--------: |
|  100*creat   |  5361  |      4331      |       2317        |  9470   |       +19%        |         +57%         |    -76%    |
|  100*start   |  9847  |     11679      |       10881       |  10699  |       -18%        |         -10%         |    -8%     |
|   100*stop   |  3422  |      1631      |       1744        |  3781   |       -52%        |         -49%         |    -10%    |
|    100*rm    |  4234  |      8850      |       10393       |  6181   |       -53%        |         -60%         |    -32%    |
