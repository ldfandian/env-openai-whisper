# Dev environment of https://github.com/openai/whisper project:
 Whisper is a general-purpose speech recognition model. It is trained on a large dataset of diverse audio and is also a multi-task model that can perform multilingual speech recognition as well as speech translation and language identification.

## build the docker image
```
docker build -t openai-whisper-devbox .
```

## run the docker container

```
docker run --rm -it -v /home/dianfan/devroot/src/:/mnt/devroot/ -v /mnt/DataExt/devroot/:/mnt/DataExt/devroot/ -w /mnt/devroot/openai-whisper/ -v ~/.ssh:/root/.ssh -v /mnt/devroot/openai-whisper/.cache/whisper/:/root/.cache/whisper/ --cpus=16 --gpus all --pids-limit=-1 --memory=84g --shm-size=84g --privileged --runtime nvidia -e NVIDIA_DRIVER_CAPABILITIES=video,compute,utility --name openai-whisper-container openai-whisper-devbox /bin/bash
```
 
## open one more shell to connect the same container
docker exec -it openai-whisper-container /bin/bash


# Extract audio (only) from movie video
```
ffmpeg -hwaccel cuda  -i <the_movie>.mkv -vn -c:a libmp3lame -q:a 0 <the_movie>.audio-only.mp3

ffmpeg -hwaccel cuda  -i /mnt/DataExt/devroot/data/openai-whisper-data/9.11.Inside.The.Presidents.War.Room.2021.REPACK.HDR.2160p.WEB.h265-RUMOUR/9.11.Inside.The.Presidents.War.Room.2021.REPACK.HDR.2160p.WEB.h265-RUMOUR.mkv -vn -c:a libmp3lame -q:a 0 /mnt/DataExt/devroot/data/openai-whisper-data/9.11.Inside.The.Presidents.War.Room.2021.REPACK.HDR.2160p.WEB.h265-RUMOUR/9.11.Inside.The.Presidents.War.Room.2021.REPACK.HDR.2160p.WEB.h265-RUMOUR.audio-only.mp3

ffmpeg -hwaccel cuda  -i /mnt/DataExt/devroot/data/openai-whisper-data/Black.Widow.2021.2160p.DSNP.WEB-DL.DDP5.1.Atmos.HDR.HEVC-CMRG/Black.Widow.2021.2160p.DSNP.WEB-DL.DDP5.1.Atmos.HDR.HEVC-CMRG.mkv -vn -c:a libmp3lame -q:a 0 /mnt/DataExt/devroot/data/openai-whisper-data/Black.Widow.2021.2160p.DSNP.WEB-DL.DDP5.1.Atmos.HDR.HEVC-CMRG/Black.Widow.2021.2160p.DSNP.WEB-DL.DDP5.1.Atmos.HDR.HEVC-CMRG.audio-only.mp3
```

# Run the AI program (in container)
```
whisper /mnt/DataExt/devroot/data/openai-whisper-data/9.11.Inside.The.Presidents.War.Room.2021.REPACK.HDR.2160p.WEB.h265-RUMOUR/9.11.Inside.The.Presidents.War.Room.2021.REPACK.HDR.2160p.WEB.h265-RUMOUR.audio-only.mp3 --model large

whisper /mnt/DataExt/devroot/data/openai-whisper-data/Black.Widow.2021.2160p.DSNP.WEB-DL.DDP5.1.Atmos.HDR.HEVC-CMRG/Black.Widow.2021.2160p.DSNP.WEB-DL.DDP5.1.Atmos.HDR.HEVC-CMRG.audio-only.mp3 --model large
```
