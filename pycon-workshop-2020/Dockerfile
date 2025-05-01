FROM pytorch/pytorch

RUN apt-get -y update && apt-get install -y git
WORKDIR /usr/src/crypten
RUN git clone https://github.com/h0rs3fa11/CrypTen.git /usr/src/crypten
RUN pip install -e .
RUN pip install -r requirements.examples.txt

RUN  pip install jupyter

# start jupyter notebook
# Tini operates as a process subreaper for jupyter to prevent kernel crashes.
ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
