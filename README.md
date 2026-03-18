Чтобы собрать бенчмарк
```bash
cd <bench-dir>
mkdir build && cd build
cmake -DCMAKE_CXX_FLAGS="-Wl,-q" -DCMAKE_C_FLAGS="-Wl,-q" ..
make
```
Запуск
```bash
./run.sh
```