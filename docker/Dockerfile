#ARG PYTORCH="2.0.0"
ARG PYTORCH="1.13.1"
#ARG CUDA="11.7"
#ARG CUDA_ALIAS="117"
ARG CUDA="11.6"
ARG CUDA_ALIAS="116"
ARG CUDNN="8"
ARG MMCV="2.0.0rc4"

FROM pytorch/pytorch:${PYTORCH}-cuda${CUDA}-cudnn${CUDNN}-devel
#RUN rm /etc/apt/sources.list.d/cuda.list
#RUN rm /etc/apt/sources.list.d/nvidia-ml.list

#ENV TORCH_CUDA_ARCH_LIST="6.0 6.1 7.0+PTX"
ENV TORCH_NVCC_FLAGS="-Xfatbin -compress-all"
ENV CMAKE_PREFIX_PATH="$(dirname $(which conda))/../"
ENV LD_LIBRARY_PATH=/usr/local/cuda-11/

RUN apt-get update && apt-get install -y git ninja-build libglib2.0-0 libsm6 libxrender-dev libxext6 libgl1-mesa-glx \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install mmagic
RUN conda clean --all
#ADD http://date.jsontest.com /etc/builddate
RUN pip install torchvision==0.14.1+cu116 torchtext==0.14.1 torchaudio==0.13.1 torchdata==0.5.1 --extra-index-url https://download.pytorch.org/whl/cu116
RUN git clone https://github.com/YananJian/s-clip.git /SCLIP
WORKDIR /SCLIP

ENV FORCE_CUDA="1"
ENV CUDA_HOME="/usr/local/cuda"
RUN pip install --upgrade pip && pip install --no-cache-dir -r requirements.txt

#RUN pip install xformers==0.0.16
#RUN pip uninstall --yes diffusers && pip install diffusers==0.13.1

RUN pip install jupyterlab
RUN apt-get update && apt-get install -y vim
#RUN pip install gradio
#RUN pip uninstall -y bitesandbytes
#RUN cd / && git clone https://github.com/TimDettmers/bitsandbytes.git /bitsandbytes
#WORKDIR /bitsandbytes
#RUN CUDA_VERSION=116 make cuda11x && python setup.py install && CUDA_VERSION=116 make cuda11x_nomatmul && python setup.py install
