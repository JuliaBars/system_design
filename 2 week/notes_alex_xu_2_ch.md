# Мысли и идеи после прочтения / просмотра

### 1. Цифры, которые желательно знать

Скорость зависит не от размера пакета, а от пропускной способности канала (bandwidth) и задержки (latency).

L1 cache reference ......................... 0.5 ns\
Branch mispredict ............................ 5 ns\
L2 cache reference ........................... 7 ns\
Mutex lock/unlock ........................... 25 ns\
Main memory reference ...................... 100 ns    
Compress 1K bytes with Zippy ............. 3,000 ns  =   3 µs - современный алгоритмы сжатия LZ4, Snappy, zstandart\
Send 2K bytes over 1 Gbps network ....... 20,000 ns  =  20 µs\
SSD random read ........................ 150,000 ns  = 150 µs\
Read 1 MB sequentially from memory ..... 250,000 ns  = 250 µs\
Round trip within same datacenter ...... 500,000 ns  = 0.5 ms\
Read 1 MB sequentially from SSD* ..... 1,000,000 ns  =   1 ms\
Disk seek ........................... 10,000,000 ns  =  10 ms\
Read 1 MB sequentially from disk .... 20,000,000 ns  =  20 ms\
Send packet CA->Netherlands->CA .... 150,000,000 ns  = 150 ms

### 2. Показатели доступности систем

В следующей таблице указано ожидаемое время простоя при различных вариантах доступности в течение одного года.
Это типичный временной интервал для коммерческих систем.

90% - 40 дней\
99% - 4 дня\
99.9% - 9 часов\
99.99% - 50 минут\
99.999% - 5 минут\
99.9999% - 30 секунд 
