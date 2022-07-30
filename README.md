# ROCALmodels
TensorFlow models repository with ROCAL support

## Steps to run SSD detection training for COCO2017 on a Rocm3.5 + TensorFlow 1.15 docker container:

### Outside the container:
```
cd $HOME
mkdir dockerMount
git clone https://github.com/LakshmiKumar23/ROCALmodels.git
sudo docker pull abishekr/mlperf_rocm3.5_tf1.15:v0.1.5
sudo docker run -it --network=host --memory=14G --device=/dev/kfd --device=/dev/dri --ipc=host --shm-size 16G --group-add video --cap-add=SYS_PTRACE --security-opt seccomp=unconfined -v $HOME/dockerMount:/media abishekr/mlperf_rocm3.5_tf1.15:v0.1.5
```

### Inside the container:
```
cd /media/ROCALmodels/models/research
./download_all.sh /media/ssdTraining/data/coco2017_tfrecords /media/ssdTraining/checkpoints
bash ./examples/SSD320_FP16_1GPU.sh /media/ssdTraining/checkpoints/ &> /media/ssdTraining/checkpoints/log.txt
```
The log is generated in log.txt.
