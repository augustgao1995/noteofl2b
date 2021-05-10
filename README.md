# noteofl2b
ubuntu 18.04 //system version needed
conda create -n l2b python=3.6
conda install numpy
//建议不要用其他命令装cmake
pip install cmake
export SCIPOPTDIR='/opt/scip'
//scip 和 soplex 解压到跟learn2branch文件夹同级的位置
tar -xzf soplex-4.0.1.tgz
cd soplex-4.0.1/
mkdir build
cmake -S . -B build -DCMAKE_INSTALL_PREFIX=$SCIPOPTDIR
make -C ./build -j 4
sudo make -C ./build install
cd ..
tar -xzf scip-6.0.1.tgz
cd scip-6.0.1/
patch -p1 < ../learn2branch/scip_patch/vanillafullstrong.patch
mkdir build
cmake -S . -B build -DSOPLEX_DIR=$SCIPOPTDIR -DCMAKE_INSTALL_PREFIX=$SCIPOPTDIR
make -C ./build -j 4
sudo make -C ./build install
conda install cython
conda install git
pip install git+https://github.com/ds4dm/PySCIPOpt.git@ml-branching
conda install scikit-learn=0.20.2
pip install git+https://github.com/jma127/pyltr@78fa0ebfef67d6594b8415aa5c6136e30a5e3395

//install gcc4.8 and g++4.8 and change the prefered version to 4.8

cd ..
git clone https://github.com/ds4dm/PySVMRank.git
cd PySVMRank
wget http://download.joachims.org/svm_rank/current/svm_rank.tar.gz
mkdir src/c
tar -xzf svm_rank.tar.gz -C src/c
pip install .//报错 collect2: error: ld returned 1 exit status    error: command 'gcc' failed with exit status 1
conda install tensorflow-gpu=1.12.0

