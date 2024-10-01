FROM nvcr.io/nvidia/nemo:24.07

ENV PYTHONUNBUFFERED=1

LABEL author="Youssef Nashed, ynashed@nvidia.com"

WORKDIR /workspace

# xformers
RUN git clone --recursive https://github.com/facebookresearch/xformers.git && cd xformers && \
    # git submodule update --init --recursive -q\
    git config --global --add safe.directory /custom-build/xformers && \
    git config --global --add safe.directory /custom-build/xformers/third_party/flash-attention && \
    git config --global --add safe.directory /custom-build/xformers/third_party/cutlass && \
    echo '' > requirements.txt && \
    pip install ninja && \
    export TORCH_CUDA_ARCH_LIST="8.0 9.0+PTX" MAX_JOBS=1 && \
    pip install -v -e .

RUN pip install deepspeed

RUN git clone https://github.com/chandar-lab/AMPLIFY.git &&\
    pip install --no-dependencies --editable AMPLIFY[dev]

ENTRYPOINT ["bash"]