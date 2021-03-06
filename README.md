# ivdm3seg

Results of our method on the non-disclosed [IVDM3Seg challenge] data as
generated by the challenge organizers using our prepared Docker containers
as described in the paper.

## Docker containers and results

- **`binary w/ latent variable`**
  * Container name: `ivdm3seg/binary`
  * [Container image](https://bit.ly/2IhNDPe)
  * [Results](results_on_nondisclosed_data/binary.xlsx)
- **`ternary`**
  * Container name: `ivdm3seg/ternary`
  * [Container image](https://bit.ly/2DIKceM)
  * [Results](results_on_nondisclosed_data/ternary.xlsx)
- **`binary w/ latent variable` (larger localizer patch size)**
  * Container name: `ivdm3seg/binary_large`
  * [Container image](https://bit.ly/2TdnaGG)
  * [Results](results_on_nondisclosed_data/binary_large.xlsx)

## How to run a Docker container

1. Download the container un-7zip it, such that you are left with an
   `IMG.tar` file
2. Load the image into Docker, i.e.,  `docker load --input IMG.tar`
3. Finnally, you can use the instructions as specified by the challenge to
   obtain segmentation results for an image:
   ```shell
   CID=`docker run -dit --runtime=nvidia --rm -v /input -v /output CONTAINER_NAME`

   docker cp TESTIMAGE_fat.nii.gz $CID:/input/fat.nii.gz
   docker cp TESTIMAGE_wat.nii.gz $CID:/input/wat.nii.gz
   docker cp TESTIMAGE_inn.nii.gz $CID:/input/inn.nii.gz
   docker cp TESTIMAGE_opp.nii.gz $CID:/input/opp.nii.gz

   docker exec $CID /challenge/run

   docker cp $CID:/output/result.nii.gz TESTIMAGE_segmentation.nii.gz

   docker stop $CID
   ```

**Note**: You need the [NVIDIA runtime] to run the Docker container.

[IVDM3Seg challenge]: https://ivdm3seg.weebly.com/
[NVIDIA runtime]: https://github.com/NVIDIA/nvidia-docker
