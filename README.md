# Apptainerized Matlab 2016b in Debian jessie image

## Build procedure

### mount matlab installation isos

at build host, do:

```
sudo mkdir /mnt/iso/1
sudo mkdir /mnt/iso/2
sudo mount -o loop ./isos/R2016b_glnxa64_dvd1.iso /mnt/iso/1
sudo mount -o loop ./isos/R2016b_glnxa64_dvd2.iso /mnt/iso/2
```

### build base image

```
sudo apptainer build debian-image.sif debian-image.def
```

### build image with X and build eseentials

Actually, `sudo` is again needed, because X installation has some weird scripts which need real root, so fakeroot is not working...

```
sudo apptainer build ./debian-image-withX.sif ./debian-image-withX.def
```

### build final image with Matlab

```
sudo apptainer build --bind /mnt/iso/1:/mnt --bind /mnt/iso/2:/root/Downloads/MathWorks/R2016b/ ./Matlab-2016b_debian-jessie.sif ./debian-image-upper.def
```

## Run Matlab

```
As matlab is in `runscript`, it's enough to execute directly the resulting `Matlab-2016b_debian-jessie.sif` image.
Installed apptainer is required.
```
