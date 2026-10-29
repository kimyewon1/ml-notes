# CIC-DDoS2019 官方 CSV：核验记录

核验时间：2026-10-29（北京时间）。数据来源：UNB/CIC 官方服务器 cicresearch.ca。

## 获取方式
- 来源页面：https://www.unb.ca/cic/datasets/ddos-2019.html，页面上的 "Download this dataset" 链到 https://cicresearch.ca/CICDataset/CICDDoS2019/
- **需要填表，不需要账号密码**：表单字段为 first_name、last_name、email、institution、job_title、country，提交（POST insert.php）后立即放行，不审核。
- 放行靠服务器端会话：没登记直接请求 download.php 返回 **403**；旧路径 `/Dataset/CSVs/*.zip` 返回 **302**，跳到数据集索引页。
- 直链（必须先在同一浏览器/会话里登记）：
  - https://cicresearch.ca/CICDataset/CICDDoS2019/download.php?file=CSVs%2FCSV-01-12.zip
  - https://cicresearch.ca/CICDataset/CICDDoS2019/download.php?file=CSVs%2FCSV-03-11.zip

## 压缩包
| 文件 | HTTP | Content-Length | 实际下载字节 | SHA-256 | unzip -t |
|---|---|---|---|---|---|
| CSV-01-12.zip | 200 | 无（服务器用 Transfer-Encoding: chunked） | 2,330,434,641 | d5224f73b59f2be783b620bc7046f4bf467c1fe226cfdbc036359ab40f32930d | 无错误 |
| CSV-03-11.zip | 200 | 无（同上） | 918,815,761 | a81d8ce59a819d13e6bfea4e4812d6d144d0572b6d2c42d8e0c0a8cf1c26c263 | 无错误 |

## 文件名说明
官方没有 `01-12-2019.csv` 这种按日期命名的单个文件。日期体现在 zip 名和文件夹名上（01-12 = 12 月 1 日训练日，03-11 = 11 月 3 日测试日），CSV 按攻击类型命名。03-11 包里还有一个 LibreOffice 锁文件 `.~lock.UDPLag.csv#`（93 字节），可以忽略。

## 逐文件统计（行数 = 数据行，不含表头；每个文件都是 88 列）
| 文件 | 解压大小（字节） | 数据行 | Label 分布 |
|---|---|---|---|
| 01-12/UDPLag.csv | 157968770 | 370605 | WebDDoS=439; UDP-lag=366461; BENIGN=3705 |
| 01-12/TFTP.csv | 9302011115 | 20107827 | TFTP=20082580; BENIGN=25247 |
| 01-12/Syn.csv | 637312127 | 1582681 | Syn=1582289; BENIGN=392 |
| 01-12/DrDoS_UDP.csv | 1506039371 | 3136802 | DrDoS_UDP=3134645; BENIGN=2157 |
| 01-12/DrDoS_SSDP.csv | 1252686219 | 2611374 | DrDoS_SSDP=2610611; BENIGN=763 |
| 01-12/DrDoS_SNMP.csv | 2172579815 | 5161377 | DrDoS_SNMP=5159870; BENIGN=1507 |
| 01-12/DrDoS_NTP.csv | 645008606 | 1217007 | DrDoS_NTP=1202642; BENIGN=14365 |
| 01-12/DrDoS_NetBIOS.csv | 1697479829 | 4094986 | DrDoS_NetBIOS=4093279; BENIGN=1707 |
| 01-12/DrDoS_MSSQL.csv | 1889181756 | 4524498 | DrDoS_MSSQL=4522492; BENIGN=2006 |
| 01-12/DrDoS_LDAP.csv | 917302277 | 2181542 | DrDoS_LDAP=2179930; BENIGN=1612 |
| 01-12/DrDoS_DNS.csv | 2133307948 | 5074413 | DrDoS_DNS=5071011; BENIGN=3402 |
| 03-11/UDPLag.csv | 319793413 | 725165 | UDP=112475; UDPLag=1873; Syn=606749; BENIGN=4068 |
| 03-11/UDP.csv | 1792797298 | 3782206 | UDP=3754680; MSSQL=24392; BENIGN=3134 |
| 03-11/LDAP.csv | 871398918 | 2113234 | LDAP=1905191; NetBIOS=202919; BENIGN=5124 |
| 03-11/MSSQL.csv | 2386225228 | 5775786 | LDAP=9931; MSSQL=5763061; BENIGN=2794 |
| 03-11/NetBIOS.csv | 1418468105 | 3455899 | NetBIOS=3454578; BENIGN=1321 |
| 03-11/Portmap.csv | 78611080 | 191694 | Portmap=186960; BENIGN=4734 |
| 03-11/Syn.csv | 1877372065 | 4320541 | Syn=4284751; BENIGN=35790 |

合计：01-12 共 50,063,112 行，03-11 共 20,364,525 行，总计 **70,427,637 行**。

注意：
- Timestamp 列里的日期是 **2018-12-01 / 2018-11-03**，不是 2019（官方原始数据如此，所有行都一致）。
- 部分文件混有别的攻击标签（如 03-11/UDPLag.csv 里大部分是 Syn），复现时要按 Label 列算，不要按文件名算。
- 每个文件内都已经混有 BENIGN 行，官方没有单独的 BENIGN 文件。

## 表头（18 个 CSV 完全一致，88 列；原文中很多列名带前导空格）
1. `Unnamed: 0`
2. `Flow ID`
3. ` Source IP`
4. ` Source Port`
5. ` Destination IP`
6. ` Destination Port`
7. ` Protocol`
8. ` Timestamp`
9. ` Flow Duration`
10. ` Total Fwd Packets`
11. ` Total Backward Packets`
12. `Total Length of Fwd Packets`
13. ` Total Length of Bwd Packets`
14. ` Fwd Packet Length Max`
15. ` Fwd Packet Length Min`
16. ` Fwd Packet Length Mean`
17. ` Fwd Packet Length Std`
18. `Bwd Packet Length Max`
19. ` Bwd Packet Length Min`
20. ` Bwd Packet Length Mean`
21. ` Bwd Packet Length Std`
22. `Flow Bytes/s`
23. ` Flow Packets/s`
24. ` Flow IAT Mean`
25. ` Flow IAT Std`
26. ` Flow IAT Max`
27. ` Flow IAT Min`
28. `Fwd IAT Total`
29. ` Fwd IAT Mean`
30. ` Fwd IAT Std`
31. ` Fwd IAT Max`
32. ` Fwd IAT Min`
33. `Bwd IAT Total`
34. ` Bwd IAT Mean`
35. ` Bwd IAT Std`
36. ` Bwd IAT Max`
37. ` Bwd IAT Min`
38. `Fwd PSH Flags`
39. ` Bwd PSH Flags`
40. ` Fwd URG Flags`
41. ` Bwd URG Flags`
42. ` Fwd Header Length`
43. ` Bwd Header Length`
44. `Fwd Packets/s`
45. ` Bwd Packets/s`
46. ` Min Packet Length`
47. ` Max Packet Length`
48. ` Packet Length Mean`
49. ` Packet Length Std`
50. ` Packet Length Variance`
51. `FIN Flag Count`
52. ` SYN Flag Count`
53. ` RST Flag Count`
54. ` PSH Flag Count`
55. ` ACK Flag Count`
56. ` URG Flag Count`
57. ` CWE Flag Count`
58. ` ECE Flag Count`
59. ` Down/Up Ratio`
60. ` Average Packet Size`
61. ` Avg Fwd Segment Size`
62. ` Avg Bwd Segment Size`
63. ` Fwd Header Length.1`
64. `Fwd Avg Bytes/Bulk`
65. ` Fwd Avg Packets/Bulk`
66. ` Fwd Avg Bulk Rate`
67. ` Bwd Avg Bytes/Bulk`
68. ` Bwd Avg Packets/Bulk`
69. `Bwd Avg Bulk Rate`
70. `Subflow Fwd Packets`
71. ` Subflow Fwd Bytes`
72. ` Subflow Bwd Packets`
73. ` Subflow Bwd Bytes`
74. `Init_Win_bytes_forward`
75. ` Init_Win_bytes_backward`
76. ` act_data_pkt_fwd`
77. ` min_seg_size_forward`
78. `Active Mean`
79. ` Active Std`
80. ` Active Max`
81. ` Active Min`
82. `Idle Mean`
83. ` Idle Std`
84. ` Idle Max`
85. ` Idle Min`
86. `SimillarHTTP`
87. ` Inbound`
88. ` Label`

## 关键字段核对
| 字段 | 是否存在 | 列号 | 原始列名 |
|---|---|---|---|
| Flow ID | 有 | 2 | `Flow ID` |
| Source IP | 有 | 3 | ` Source IP`（前导空格） |
| Destination IP | 有 | 5 | ` Destination IP`（前导空格） |
| Timestamp | 有 | 8 | ` Timestamp`（前导空格） |
| Label | 有 | 88 | ` Label`（前导空格） |

第 1 列 `Unnamed: 0` 是 pandas 写出时留下的索引列，官方文件本来就有，算在 88 列里。
