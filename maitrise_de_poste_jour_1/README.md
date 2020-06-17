# Maitrise de poste day 1
## Self-footprinting
### Host OS
```shell
PS C:\Users\cleme> Get-CimInstance -ClassName Win32_ComputerSystem

Name             PrimaryOwnerName    Domain              TotalPhysicalMemory Model               Manufacturer
----             ----------------    ------              ------------------- -----               ------------
MSI              clement.dournetd... WORKGROUP           17017856000         GL65 9SE            Micro-Star Inter...
```
Le nom de la machine est MSI.
```shell
PS C:\Users\cleme> Get-WmiObject Win32_OperatingSystem


SystemDirectory : C:\WINDOWS\system32
Organization    :
BuildNumber     : 18363
RegisteredUser  : clement.dournetd@outlook.fr
SerialNumber    : 00325-81435-02688-AAOEM
Version         : 10.0.18363
```
l'OS de la machine est Windows 10 en version 10.0.18363
```shell
PS C:\Users\cleme> Get-CimInstance -ClassName Win32_Processor

DeviceID Name                                     Caption                                MaxClockSpeed SocketDesigna
                                                                                                       tion
-------- ----                                     -------                                ------------- -------------
CPU0     Intel(R) Core(TM) i7-9750H CPU @ 2.60GHz Intel64 Family 6 Model 158 Stepping 13 2592          U3E1
```
Le modèle du processeur est Intel(R) Core(TM) i7-9750H
```shell
PS C:\Users\cleme> Get-CimInstance win32_physicalmemory | Format-Table Manufacturer,Banklabel,Configuredclockspeed,Devicelocator,Capacity,Serialnumber -autosize

Manufacturer Banklabel Configuredclockspeed Devicelocator    Capacity Serialnumber
------------ --------- -------------------- -------------    -------- ------------
SK Hynix     BANK 0                    2667 ChannelA-DIMM0 8589934592 7296DDF4
SK Hynix     BANK 2                    2667 ChannelB-DIMM0 8589934592 52DA7DC6
```
L'ordinateur est équipé de 2 barrettes de RAM de 4go chacune, soit 8go au total. La marque est SK Hynix.
### Devices
```shell
PS C:\Users\cleme> WMIC CPU Get DeviceID,NumberOfCores,NumberOfLogicalProcessors
DeviceID  NumberOfCores  NumberOfLogicalProcessors
CPU0      6              12
```
Le nom `Intel(R) Core(TM) i7-9750H` veut dire qu'il s'agit d'un processeur i7 de 9ème génération. Il est équipé de 6 coeur et 12 processeurs logiques.
```shell
PS C:\Users\cleme> wmic SOUNDDEV get Manufacturer,Name
Manufacturer          Name
Realtek               Realtek High Definition Audio
NVIDIA                NVIDIA Virtual Audio Device (Wave Extensible) (WDM)
Intel(R) Corporation  Son Intel(R) pour écrans
NVIDIA                NVIDIA High Definition Audio
```
Le fabriquant de mes enceintes est Realtek.
```shell
PS C:\Users\cleme> get-Disk

Number Friendly Name                                                                                                                      Serial Number                    HealthStatus         OperationalStatus      Total Size Partition
                                                                                                                                                                                                                                  Style
------ -------------                                                                                                                      -------------                    ------------         -----------------      ---------- ----------
0      WDC PC SN520 SDAPNUW-512G-1032                                                                                                     E823_8FA6_BF53_0001_001B_448B... Healthy              Online                  476.94 GB GPT
```
La marque et le modèle sont WDC PC SN520 SDAPNUW-512G-1032.
```shell
PS C:\Users\cleme> get-Partition


   DiskPath : \\?\scsi#disk&ven_nvme&prod_wdc_pc_sn520_sda#5&1d1fa537&0&000000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}

PartitionNumber  DriveLetter Offset                                                                                                   Size Type
---------------  ----------- ------                                                                                                   ---- ----
1                            1048576                                                                                                300 MB System
2                            315621376                                                                                              128 MB Reserved
3                C           449839104                                                                                            457.9 GB Basic
4                            492117688320                                                                                           900 MB Recovery
5                            493061406720                                                                                         17.74 GB Recovery
```
L'ordinateur est équipé d'un disque principal, divisé en 5 partitions.
```shell
PS C:\Users\cleme> get-VOlume

DriveLetter FriendlyName FileSystemType DriveType HealthStatus OperationalStatus SizeRemaining     Size
----------- ------------ -------------- --------- ------------ ----------------- -------------     ----
            WinRE tools  NTFS           Fixed     Healthy      OK                    442.38 MB   900 MB
            BIOS_RVY     NTFS           Fixed     Healthy      OK                    675.05 MB 17.74 GB
C           Windows      NTFS           Fixed     Healthy      OK                     88.83 GB 457.9 GB
```
Chaque partition est configuré avec le système de ficheirs NTFS. La partition WinRE tools correspond à la partition comprenant l'environnement de récupération de Windows. La partition BIOS_RVY est la partition de récupération de mon système. La partition Windows est la partition comprenant mon système et mes fichiers.

### Network
```shell
PS C:\Users\cleme> Get-NetAdapter

Name                      InterfaceDescription                    ifIndex Status       MacAddress             LinkSpeed
----                      --------------------                    ------- ------       ----------             ---------
VirtualBox Host-Only ...2 VirtualBox Host-Only Ethernet Adap...#2      28 Up           0A-00-27-00-00-1C         1 Gbps
Ethernet 5                AnchorFree TAP-Windows Adapter V9            26 Disconnected 00-FF-D7-F1-F6-FD       100 Mbps
Wi-Fi                     Intel(R) Wireless-AC 9560 160MHz             25 Up           5C-87-9C-D7-C1-ED     866.7 Mbps
Ethernet 4                VirtualBox Host-Only Ethernet Adapter        20 Up           0A-00-27-00-00-14         1 Gbps
Ethernet 2                Realtek PCIe GbE Family Controller #2        18 Disconnected 00-D8-61-85-7B-47          0 bps
VMware Network Adapte...1 VMware Virtual Ethernet Adapter for ...      16 Up           00-50-56-C0-00-01       100 Mbps
Connexion réseau Blue...2 Bluetooth Device (Personal Area Ne...#2      15 Disconnected 5C-87-9C-D7-C1-F1         3 Mbps
VirtualBox Host-Only ...3 VirtualBox Host-Only Ethernet Adap...#3      13 Up           0A-00-27-00-00-0D         1 Gbps
VirtualBox Host-Only ...4 VirtualBox Host-Only Ethernet Adap...#4      11 Up           0A-00-27-00-00-0B         1 Gbps
Connexion au réseau local TAP-Windows Adapter V9                       10 Disconnected 00-FF-32-59-40-40         1 Gbps
VMware Network Adapte...8 VMware Virtual Ethernet Adapter for ...       7 Up           00-50-56-C0-00-08       100 Mbps
```
Les cartes commençant par VirtualBox et VMware correspondent aux cartes virtuels que j'ai créé pour mes différentes VMs. La carte Ethernet 2 correspond à ma carte ethernet et la carte Wi-Fi correspond à ma carte wifi.

Voici la liste des diffrents ports en écoute : 
```shell
PS C:\Users\cleme> netstat -a

Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    0.0.0.0:135            MSI:0                  LISTENING
  TCP    0.0.0.0:443            MSI:0                  LISTENING
  TCP    0.0.0.0:445            MSI:0                  LISTENING
  TCP    0.0.0.0:808            MSI:0                  LISTENING
  TCP    0.0.0.0:902            MSI:0                  LISTENING
  TCP    0.0.0.0:912            MSI:0                  LISTENING
  TCP    0.0.0.0:2869           MSI:0                  LISTENING
  TCP    0.0.0.0:4424           MSI:0                  LISTENING
  TCP    0.0.0.0:5040           MSI:0                  LISTENING
  TCP    0.0.0.0:5357           MSI:0                  LISTENING
  TCP    0.0.0.0:7680           MSI:0                  LISTENING
  TCP    0.0.0.0:9001           MSI:0                  LISTENING
  TCP    0.0.0.0:49664          MSI:0                  LISTENING
  TCP    0.0.0.0:49665          MSI:0                  LISTENING
  TCP    0.0.0.0:49666          MSI:0                  LISTENING
  TCP    0.0.0.0:49667          MSI:0                  LISTENING
  TCP    0.0.0.0:49686          MSI:0                  LISTENING
  TCP    0.0.0.0:49703          MSI:0                  LISTENING
  TCP    127.0.0.1:5939         MSI:0                  LISTENING
  TCP    127.0.0.1:6463         MSI:0                  LISTENING
  TCP    127.0.0.1:7912         MSI:7913               ESTABLISHED
  TCP    127.0.0.1:7913         MSI:7912               ESTABLISHED
  TCP    127.0.0.1:7959         MSI:65001              ESTABLISHED
  TCP    127.0.0.1:7991         MSI:7992               ESTABLISHED
  TCP    127.0.0.1:7992         MSI:7991               ESTABLISHED
  TCP    127.0.0.1:8116         MSI:8117               ESTABLISHED
  TCP    127.0.0.1:8117         MSI:8116               ESTABLISHED
  TCP    127.0.0.1:8119         MSI:8120               ESTABLISHED
  TCP    127.0.0.1:8120         MSI:8119               ESTABLISHED
  TCP    127.0.0.1:8123         MSI:8124               ESTABLISHED
  TCP    127.0.0.1:8124         MSI:8123               ESTABLISHED
  TCP    127.0.0.1:8189         MSI:0                  LISTENING
  TCP    127.0.0.1:8189         MSI:8267               ESTABLISHED
  TCP    127.0.0.1:8267         MSI:8189               ESTABLISHED
  TCP    127.0.0.1:8307         MSI:0                  LISTENING
  TCP    127.0.0.1:27015        MSI:0                  LISTENING
  TCP    127.0.0.1:28385        MSI:0                  LISTENING
  TCP    127.0.0.1:49668        MSI:49669              ESTABLISHED
  TCP    127.0.0.1:49669        MSI:49668              ESTABLISHED
  TCP    127.0.0.1:50911        MSI:0                  LISTENING
  TCP    127.0.0.1:50912        MSI:0                  LISTENING
  TCP    127.0.0.1:65001        MSI:0                  LISTENING
  TCP    127.0.0.1:65001        MSI:7959               ESTABLISHED
  TCP    192.168.1.42:139       MSI:0                  LISTENING
  TCP    192.168.1.42:7680      PC-de-clment:58706     TIME_WAIT
  TCP    192.168.1.42:7962      40.67.254.36:https     ESTABLISHED
  TCP    192.168.1.42:8675      162.159.130.235:https  ESTABLISHED
  TCP    192.168.1.42:12612     162.159.135.234:https  ESTABLISHED
  TCP    192.168.1.42:13191     162.159.130.233:https  ESTABLISHED
  TCP    192.168.1.42:13203     ec2-3-112-116-223:https  TIME_WAIT
  TCP    192.168.1.42:13211     ec2-3-120-69-5:https   TIME_WAIT
  TCP    192.168.1.42:13215     ec2-3-120-69-5:https   TIME_WAIT
  TCP    192.168.1.42:13231     40.79.65.237:https     ESTABLISHED
  TCP    192.168.1.42:13233     20.186.48.46:https     ESTABLISHED
  TCP    192.168.1.42:13241     par10s34-in-f4:https   TIME_WAIT
  TCP    192.168.1.42:13244     ec2-3-120-94-69:https  ESTABLISHED
  TCP    [::]:135               MSI:0                  LISTENING
  TCP    [::]:443               MSI:0                  LISTENING
  TCP    [::]:445               MSI:0                  LISTENING
  TCP    [::]:808               MSI:0                  LISTENING
  TCP    [::]:2869              MSI:0                  LISTENING
  TCP    [::]:4424              MSI:0                  LISTENING
  TCP    [::]:5357              MSI:0                  LISTENING
  TCP    [::]:7680              MSI:0                  LISTENING
  TCP    [::]:9001              MSI:0                  LISTENING
  TCP    [::]:49664             MSI:0                  LISTENING
  TCP    [::]:49665             MSI:0                  LISTENING
  TCP    [::]:49666             MSI:0                  LISTENING
  TCP    [::]:49667             MSI:0                  LISTENING
  TCP    [::]:49686             MSI:0                  LISTENING
  TCP    [::]:49703             MSI:0                  LISTENING
  TCP    [::1]:8307             MSI:0                  LISTENING
  TCP    [::1]:50234            MSI:0                  LISTENING
  UDP    0.0.0.0:67             *:*
  UDP    0.0.0.0:500            *:*
  UDP    0.0.0.0:3702           *:*
  UDP    0.0.0.0:3702           *:*
  UDP    0.0.0.0:3702           *:*
  UDP    0.0.0.0:3702           *:*
  UDP    0.0.0.0:4500           *:*
  UDP    0.0.0.0:5050           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5355           *:*
  UDP    0.0.0.0:50839          *:*
  UDP    0.0.0.0:51399          *:*
  UDP    0.0.0.0:53241          *:*
  UDP    0.0.0.0:53906          *:*
  UDP    0.0.0.0:55591          *:*
  UDP    0.0.0.0:58550          *:*
  UDP    0.0.0.0:61831          *:*
  UDP    10.3.2.1:5353          *:*
  UDP    10.4.1.1:5353          *:*
  UDP    127.0.0.1:1900         *:*
  UDP    127.0.0.1:10040        *:*
  UDP    127.0.0.1:53722        *:*
  UDP    127.0.0.1:60906        *:*
  UDP    127.0.0.1:60907        *:*
  UDP    127.0.0.1:63257        *:*
  UDP    192.168.1.42:137       *:*
  UDP    192.168.1.42:138       *:*
  UDP    192.168.1.42:1900      *:*
  UDP    192.168.1.42:2177      *:*
  UDP    192.168.1.42:5353      *:*
  UDP    192.168.1.42:63256     *:*
  UDP    192.168.17.1:5353      *:*
  UDP    192.168.37.1:5353      *:*
  UDP    192.168.56.1:5353      *:*
  UDP    192.168.124.1:5353     *:*
  UDP    [::]:500               *:*
  UDP    [::]:3702              *:*
  UDP    [::]:3702              *:*
  UDP    [::]:3702              *:*
  UDP    [::]:3702              *:*
  UDP    [::]:4500              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5355              *:*
  UDP    [::]:50840             *:*
  UDP    [::]:51399             *:*
  UDP    [::]:53907             *:*
  UDP    [::]:55592             *:*
  UDP    [::]:61832             *:*
  UDP    [::1]:1900             *:*
  UDP    [::1]:5353             *:*
  UDP    [::1]:5353             *:*
  UDP    [::1]:63255            *:*
  UDP    [fe80::60ab:78bf:73c7:725a%25]:1900  *:*
  UDP    [fe80::60ab:78bf:73c7:725a%25]:2177  *:*
  UDP    [fe80::60ab:78bf:73c7:725a%25]:63254  *:*
```

### Users
Voici la liste des utilisateurs présents sur l'ordinateur : 
```shell
PS C:\Users\cleme> Get-localuser

Name               Enabled Description
----               ------- -----------
Administrateur     False   Compte d’utilisateur d’administration
cleme              True
DefaultAccount     False   Compte utilisateur géré par le système.
Invité             False   Compte d’utilisateur invité
WDAGUtilityAccount False   Compte d’utilisateur géré et utilisé par le système pour les scénarios Windows Defender Application Guard.
```
Le compte full admin est le compte `Administrateur`.

### Processus
```shell
PS C:\Users\cleme> Get-Process

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
    218      17     3220      11364       1,02   6060   4 AppleMobileDeviceProcess
    519      43    30020      41428       0,53  21140   4 ApplicationFrameHost
    447      25    26804      29964     260,81  10740   0 audiodg
    733      52    38352      23612      63,33   7368   4 bdagent
    215      12     4008       9628             15156   0 bdredline
   2238     160   617432     358368              2108   0 bdservicehost
    915      50    48000      51196              2960   0 bdservicehost
    360      20     9316      14156              6952   0 bdservicehost
    326      29    11320      19708       0,69  15252   4 BdVpnApp
    841      44    35200      38096              2996   0 BdVpnService
    157       9     3344       8732       0,08   1004   4 CompPkgSrv
    118       7     6420       4756              6296   0 conhost
    124       9     6640       1040       0,06  18776   4 conhost
    269      16     8484      19652      10,53  22324   4 conhost
    918      29     2292       6184               984   0 csrss
    773      22     3084       6160             13180   4 csrss
    499      19     6264      15528       7,89  20244   4 ctfmon
    513      19     9888      20212              2776   0 dasHost
    763      36    14920      25640              2988   0 DevMgmtService
    325      25    11496      18812       5,92   7428   4 Discord
    996     129   272292     202056   1 140,97  18140   4 Discord
   1380      53    39980      74452      82,59  18408   4 Discord
    247      20     9632      12608       0,03  19292   4 Discord
    960      36   121584     115016      94,91  21512   4 Discord
    475      29    14376      25956       5,08  22704   4 Discord
    248      15     3016      10912             23012   0 DiscoverySrv
    247      22     5304      12828       0,13   2580   4 dllhost
    154      11     3796      10060       0,03   8320   4 dllhost
    165      12     3844      11000       0,20   9456   4 dllhost
    195      16     3552      10232             19616   0 dllhost
   1560      59   183248      82084      10,39  18376   4 Dragon Center
    818      41    34456      42916              6912   0 DSAService
    486      34    34736      32564             11016   0 DSAUpdateService
   1405      65   270472     187292             20408   4 dwm
    348      17     6128      12204              6864   0 EvtEng
   3944     130   102272     161220      54,73   1648   4 explorer
   1406      85   161996     314916      16,20   1176   4 firefox
    630      49    92704     138464       1,02  11168   4 firefox
    503      28    61040      75116       9,47  14648   4 firefox
    700      66   194776     244136      39,95  15996   4 firefox
    475      34    23496      50704       0,14  21572   4 firefox
    515      39    32116      72100       0,33  22144   4 firefox
     32       5     1492       2344              1212   0 fontdrvhost
     32      11     6356      12448             10812   4 fontdrvhost
    430      30    61048      49004             17704   0 IAStorDataMgrSvc
    293      21    34712      30728       0,11  12528   4 IAStorIcon
     88       6     1224       3900              6936   0 ibtsiva
      0       0       60          8                 0   0 Idle
    415      33    15712      43584       0,19  13688   4 IGCC
    756      38    47228      58300       1,25  10744   4 IGCCTray
    169       9     2056       7036              2252   0 igfxCUIService
    836      24     7136      23320       1,16  17036   4 igfxEM
    138       8     1512       5484              7116   0 IntelCpHDCPSvc
    134       7     1600       5864              7956   0 IntelCpHeciSvc
    145      11     2008       5436              3084   0 jhi_service
    368      20     4076      14284       0,30   5576   4 jucheck
    266      17     2948      14744       0,06  20352   4 jusched
    263      16     4172      10700             18164   0 LMS
    536      25    15016      53868       0,75   8544   4 LockApp
   1964      44    10832      22684              1044   0 lsass
      0       0     1568     351676              3440   0 Memory Compression
    889      49    50708      39632       0,95   5956   4 Microsoft.Photos
    288      14    13596      14096              6928   0 MSIAPService
    198      13     2252       8116              6888   0 MSIService
    553      19    13168      20312              5940   0 NahimicService
   1238      29    14636       3292       3,63  19360   4 NahimicSvc32
    303      18     7288       2164       1,80   3300   4 NahimicSvc64
    341      19     7080      22596       0,42   6092   4 nvcontainer
    502      49    37320      38248      12,09  13124   4 nvcontainer
    710     288    13504      32500             21248   0 nvcontainer
    316      14     4928      14412              2724   0 NVDisplay.Container
    654      36    34324      36524              7604   4 NVDisplay.Container
    494      27    35028      29824       0,48   1612   4 NVIDIA Share
    715      35    20644      48140       3,67  19188   4 NVIDIA Share
    333      33    57004      58460       0,61  22420   4 NVIDIA Share
    613      77    31032      10088       1,86  16468   4 NVIDIA Web Helper
    224      13     2940      11380       0,42   7708   4 nvsphelper64
    432      61    34668      29628              6972   0 OneApp.IGCC.WinService
    150      11     2796       8240       0,02  15984   4 openvpn-gui
    143       8     1356       4928              6920   0 openvpnserv
    787      42   125576     142344       4,48   2948   4 powershell
    233      27    25032      14668              4780   0 PresentationFontCache
    356      53     7820      14680              7024   0 ProductAgentService
      0      14    11676      94952               144   0 Registry
    302      19     7960      21476       0,27  17936   4 RemindersServer
    140       8     1580       5820              6996   0 RstMwService
    495      12     3468       8824              7032   0 RtkAudUService64
    232      13     3576       8480       0,06  16532   4 RtkAudUService64
    811      39    14080      44000       8,19   1784   4 RuntimeBroker
    490      29    11000      38556       2,27   4920   4 RuntimeBroker
    227      17     5884      21852       0,25   7472   4 RuntimeBroker
    415      24    10828      28256       0,47   9264   4 RuntimeBroker
    194      13     4320      10608       0,05  13268   4 RuntimeBroker
    368      24     5692      25360       4,50  14772   4 RuntimeBroker
    382      27     9688      29696       1,56  16344   4 RuntimeBroker
    212      15     4424      14548       0,13  17392   4 RuntimeBroker
    316      20     6464      26220       0,23  19124   4 RuntimeBroker
    307      20     6856      24120       0,73  22124   4 RuntimeBroker
    508      54    82904      47840      19,92  21496   4 Scanner Mouse
    219      22     5684      17200       0,08   1964   4 Scanner Mouse Monitoring
    875      80    66768      76612              8748   0 SearchIndexer
   1820     116   124660     205668      11,23   7728   4 SearchUI
    183      13     4052      14040       0,03   1872   4 SecurityHealthHost
    546      18     6012      15028             16052   0 SecurityHealthService
    148      11     3324       8960       0,02  17672   4 SecurityHealthSystray
    857      39    26964      36816              7144   0 Sendevsvc
    878      11     6404       9256               988   0 services
    274      15     4428       5820       0,06  18920   4 SettingSyncHost
     89       6     3608       5956              2448   0 SgrmBroker
    709      31    18616      65576       4,83  14360   4 ShellExperienceHost
    705      27    10764      32408       7,89   2560   4 sihost
   1086     101   204196      17120       2,17   8348   4 SkypeApp
    150       8     2172       1112       0,02   3976   4 SkypeBackgroundHost
    436      35    18560      30740       0,31   6484   4 smartscreen
     53       3     1180       1104               680   0 smss
    551      29     9520      18888              5664   0 spoolsv
    194      12     2136       5716              6400   0 ss_conn_service
    194      12     2196       5768              7084   0 ss_conn_service2
    797      39    49264     109076      12,08  11476   4 StartMenuExperienceHost
   1170      17     4192       9112               380   0 svchost
    444      14    15792      16448               768   0 svchost
    171       7     1780       5464              1092   0 svchost
     86       5      916       3504              1164   0 svchost
   1498      29    18960      34828              1188   0 svchost
   1662      21    13180      19688              1268   0 svchost
    316      10     3168       7992              1324   0 svchost
    271      25     2492       7392              1564   0 svchost
    269      30     2296      11160              1572   0 svchost
    275      19     3116       9320              1576   0 svchost
    259      13     2920       9796              1744   0 svchost
    160      10     2432      10940              1752   0 svchost
    326      10     2496       7128              1896   0 svchost
    184       9     2136       6948              1952   0 svchost
    413      19     7180      13496              2012   0 svchost
    487      20     4844      17116              2060   0 svchost
    225      13     3052      10804              2072   0 svchost
    244      12     2440       7512              2084   0 svchost
    226      14     2352       8460              2096   0 svchost
    279      20     5608      13120              2308   0 svchost
    393      12     3244       9744              2320   0 svchost
    176      33     6304       9628              2328   0 svchost
    221      10     2576       6984              2436   0 svchost
    208       9     2412       7124              2536   0 svchost
    144      11     3196       7716              2612   0 svchost
    402      17     5716      12500              2656   0 svchost
    296      13     3828       8564              2716   0 svchost
    125       8     1608       6144              2764   0 svchost
    222      12     2756      12420              3276   0 svchost
    265       7     1364       5256              3288   0 svchost
    331      10     2632       8324              3380   0 svchost
    167      11     1808       6764              3388   0 svchost
    188       9     2276       6884              3572   0 svchost
    226      12     2552       9728              3848   0 svchost
    204      11     2404       7836              4032   0 svchost
    452      18    11300      21480              4280   0 svchost
    305      16     3504       8592              4492   0 svchost
    691      15     5988      15228              4936   0 svchost
    142       8     3892       9332              5040   0 svchost
    318      15     5212      17872              5052   0 svchost
    186       9     1840       6624              5376   0 svchost
    141      10     1920       5848              5520   0 svchost
    377      15     3292       9028              5536   0 svchost
    268      13    13516      21260              5544   0 svchost
    531      24     7136      17236              5880   0 svchost
    284      18     3800      13792              6028   0 svchost
    426      33    16972      20540              6232   0 svchost
    181      10     1976       6300              6268   0 svchost
    386      22    42620      50712              6848   0 svchost
    341      30     7776      17724              6856   0 svchost
    263      13     2732       6964              6872   0 svchost
    559      24    21820      29384              6904   0 svchost
    128       7     1344       4908              6944   0 svchost
    135       9     1600       5396              6964   0 svchost
    319      14     3372       9536              6988   0 svchost
    438      21     5392      20792              7176   0 svchost
    216      12     2576       5876              7656   0 svchost
    138       9     1752       5348              8100   0 svchost
    405      27     3640      11080              8124   0 svchost
    524      24    11360      29208       5,84   8948   4 svchost
    551      35    12832      25028              9388   0 svchost
    219      12     2812       9840              9672   0 svchost
    269      15     3964      10604              9772   0 svchost
    467      27     7080      19804             10308   0 svchost
    168      12     2916       6896             10668   0 svchost
    373      20     4420      15120             10720   0 svchost
    176      10     2196       7620             10964   0 svchost
    177     122     3436       7008             11072   0 svchost
    159      12     3640       8868             12356   0 svchost
    758      20    11012      33648             12428   0 svchost
    510      32     7512      25104       1,02  12944   4 svchost
    145      10     3392       7836             13376   0 svchost
    162      14     2516       7048             14100   0 svchost
    366      17     3788      11996             14188   0 svchost
    263      20     3856       8852             14208   0 svchost
    311      20     5140      19620             14724   0 svchost
    135      11     3380       8508             15548   0 svchost
    330      18     6260      14004             15760   0 svchost
    120      11     3240       7060       0,03  16796   4 svchost
    574      34    10736      40504       9,34  17192   4 svchost
    353      13     3716      10060             17536   0 svchost
    164      12     3212       6200             17728   0 svchost
    232      15     4080      11024             18344   0 svchost
    188      17     8272       9628             18836   0 svchost
    492      20    13040      19716             19224   0 svchost
    177      14     3172      10412             19716   0 svchost
    351      29    11068      20316             20056   0 svchost
    190      12     4168      12392             20808   0 svchost
    278      17     5240      13020             20820   0 svchost
    311      19     4672      23508       0,44  21348   4 svchost
    162      12     3472       8576       0,41  21448   4 svchost
    119       9     2968       6588             22632   0 svchost
   6079       0      204       3468                 4   0 System
   1012      44    30896      67808       1,08  22972   4 SystemSettings
    329      59    15992      25012       0,94  23468   4 taskhostw
    675      36    38636      63976       7,28  18324   4 Taskmgr
    416     570     7508      16640              7220   0 TeamViewer_Service
    137       8     2088       6820              4412   0 unsecapp
    336      20    13928      18232              6300   0 updatesrv
    776      40    22596        268       0,31  16536   4 Video.UI
    174      12     2740       6916              7092   0 vmnat
     87       8     7752       4300              6360   0 vmnetdhcp
    325      17     6920      10992              7044   0 vmware-authd
    459      34    34096      27980             11588   0 vmware-hostd
    193      19     4552       9892       0,03  22196   4 vmware-tray
    221      13     3044       9228              7100   0 vmware-usbarbitrator64
    515      23    12468      43496       1,08  23004   4 WindowsInternal.ComposableShell.Experiences.TextInput.InputApp
    163      11     1716       6300               392   0 wininit
    279      12     2820       9876             10452   4 winlogon
   1098      67    56608      67816       0,72  21608   4 WinStore.App
    341      16     4368      12276              6276   0 wlanext
    357      24     8052      23412              4528   0 WmiPrvSE
    681      32    17040       9760       0,25   8076   4 YourPhone
```
Le service explorer permet d'avoir le bureau windows, la barre des tâches et les fenêtres de l'explorateur de fichiers. le service System correspond au service permettant de faire fonctionner le système. Les services svchosts sont des services système.
Les services lancés par l'utilisateur full admin ont un SI à 0 et ceux lancés par l'utilisateur ont un SI à 4.

## Scripting
### Script 1
```shell

$nom = wmic DESKTOPMONITOR get systemName
$nom = $nom[2]
$ip = wmic NICCONFIG get IPAddress
$ip = $ip[8]
$os = wmic OS get SystemDirectory 
$os = $os[2]
$version_os = wmic OS get Version 
$version_os = $version_os[2]
$heure = wmic OS get LastBootUpTime
$heure = $heure[2]
$ajour = wmic OS get status
$ajour = $ajour[2]


function Volume {
    $os =  Get-WmiObject Win32_logicaldisk
    foreach($element in $os){
        $stockage_utilise = [math]::Round($element.Size/1000000000,2)
        $stockage_libre = [math]::Round($element.FreeSpace/1000000000,2)
        Write-Output "Le stockage utilise de la machine est $stockage_utilise Go"
        Write-Output "Le stockage libre de la machine est $stockage_libre Go"
    }
}



function Ram {
    $os = Get-WmiObject Win32_OperatingSystem
    $RAM_utilise = [math]::Round(($os.TotalVisibleMemorySize-$os.FreePhysicalMemory) / 1000000, 2)
    $RAM_libre = [math]::Round((Get-WmiObject win32_operatingsystem).FreePhysicalMemory / 1000000, 2)
    Write-Output "La RAM utilise de la machine est $RAM_utilise Mo"
    Write-Output "La RAM libre de la machine est $RAM_libre Mo"
}


$utilisateur = Get-localuser


function Ping_Moyenne {
    $ping = Test-Connection -count 10 8.8.8.8
    $moyenne = ($ping | Measure-Object ResponseTime -average -maximum)
    $calcul = [math]::Round($moyenne.average, 2)
    Write-Output "Le temps moyenne vers 8.8.8.8 est $calcul secondes"
}

echo "Le nom de la machine est $nom"
echo "L'adresse IP sur la machine est $ip"
echo "L'OS de la machine est $os"
echo "La version de l'OS de la machine est $version_os"
echo "Machine allumé depuis $heure"
echo "Version de l'OS à jour ? $ajour" 
$(Volume)
$(RAM)
echo "Les utilisateurs sur cette machine sont $utilisateur"
$(Ping_Moyenne)

Write-Host -Object ('The key that was pressed was: {0}' -f [System.Console]::ReadKey().Key.ToString());
```

### Script 2
```shell
$valeur = Read-Host "Entrer la durée avant d'executer le script en seconde"
$eteindre = Read-Host "Si vous voulez eteindre votre ordinateur taper oui"
Start-Sleep -Seconds $valeur
if ($eteindre -eq "oui") {
    Stop-Computer
} else {
    rundll32.exe user32.dll,LockWorkStation
}
```

## Gestionnaire de softs
L'usage d'un gestionnaire de paquets permet de télécharger des programmes qui sont vérifiés avant d'être publiés, ce qui limite le nombre de téléchargements de programmes malveillants, et ainsi protège les utilisateurs.

```shell
PS C:\Users\cleme> choco list -l
Chocolatey v0.10.15
chocolatey 0.10.15
chocolatey-core.extension 1.3.5.1
chocolatey-dotnetfx.extension 1.0.1
chocolatey-visualstudio.extension 1.8.1
chocolatey-windowsupdate.extension 1.0.4
dotnetfx 4.8.0.20190930
KB2919355 1.0.20160915
KB2919442 1.0.20160915
KB2999226 1.0.20181019
KB3033929 1.0.5
KB3035131 1.0.3
python2 2.7.18
vcredist140 14.25.28508.3
visualstudio-installer 2.0.1
visualstudio2017-workload-vctools 1.3.2
visualstudio2017buildtools 15.9.22.0
16 packages installed.
```
Nous pouvons remarquer qu'il y a 16 paquets installés sur mon PC.

```shell
PS C:\Users\cleme> choco source
Chocolatey v0.10.15
chocolatey - https://chocolatey.org/api/v2/ | Priority 0|Bypass Proxy - False|Self-Service - False|Admin Only - False.
```
La source des paquets est https://chocolatey.org/api/v2/

## Partage de fichiers
Après avoir fait clic-droit, propriétés, partager, et avoir défini les autorisations, le partage de fichiers est désormais fonctionnel. Un service supplémentaire nommé svchost est apparu, signifiant que le service est bien activé0

## Chiffrement et notions de confiance : 

L'information principale d'un certificat est la clé publique fournie par le site.

Les autres informations importantes contenu dans un certificat sont l'url du site, le nom de l'entreprise de certification, la signature de l'entreprise de certification et la date d'expiration du certificat.

## TLS

Une connexion HTTPS garantit une connexion sécurisée avec le site, donc un échange d'informations de manière sécurisée.

Le cadenas vert signifie que les informations transmises sont chiffrées.

Choix du certificat de Gitlab : 
* le nom du site :arrow_right: donne le nom du site auquelle on accède
* nom de l'émetteur :arrow_right: donne le nom de l'entreprise qui a émis le certificat
* validité :arrow_right: période de validité du certificat
* noms alternatifs :arrow_right: autres noms du serveur dns du site
* informations de la clé :arrow_right: l'algorithme utilisé, la taille...
* diverses informations
* empreintes numériques :arrow_right: montres les clés publiques du site.

Ce qui permet de faire confiance en un site c'est s'avoir les différentes clés, les différentes infos sur le sites et de savoir par qui le certificat a été émis.

## SSH
### Client
on génère une clé pusblique et une clé privée avec la commande `ssh-keygen`. On dépose la clé publique dans le fichier `.ssh/authorized_keys`. Il est impératif de déposer uniquement la clé publique car la clé privée permet de déchiffrer les données transmises, donc déposer cette clé reviendrait à donner la possibilité à n'importe qui d'accéder aux informations. Une fois la clé publique copiée, la connexion en SSH ne nécéssitera plus l'entrée du mot de passe. Les autorisations de ce fichier sont 644, soit l'autorisation de lecture et d'écriture par le propriétaire du fichier, et uniquement une autorisation de lecture pour les utilisateurs du même groupe ou les autres utilisateurs.

Le fingerprint ssh permet de déceller lorsque la clé du serveur a changé et ne correspond donc plus à celle enregistrée.
```shell
Host toto
        HostName 192.168.1.51
        User user
        Port 22
	    IdentityFile .ssh\id_rsa
```
### SSH tunnels
![](https://i.imgur.com/ArDhvti.png)

![](https://i.imgur.com/GJA5nKj.png)

Le tunnel SSH est donc bien fonctionnel.

### SSH jumps
Le SSH jump permet de se connecter à une machine à distance en passant par une machine intermédiaire, ce qui permet donc d'isoler la machine sur laquelle on souhaite se connecter, et ainsi améliorer la sécurité de la connexion.
```shell
Host toto
        HostName 192.168.1.51
        User user
        Port 22
	IdentityFile .ssh\id_rsa

Host jump
        HostName 10.2.1.3
	User user
	Port 22
	IdentityFile .ssh\id_rsa
	ProxyCommand ssh -q -W %h:%p toto
```

