FROM jupyterhub/k8s-singleuser-sample:0.8.2

USER root

RUN cd /tmp && \
    mkdir -p /opt/conda2 && \
    chown $NB_USER:$NB_GID /opt/conda2 && \
    apt update -y && \
    apt install -y build-essential && \
    apt clean && \
    apt autoclean && \
    apt autoremove

RUN cd /tmp && \
	wget http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz && \
	tar zxvf ta-lib-0.4.0-src.tar.gz && \
	cd ta-lib && \
	./configure --prefix=/usr && \
	make && \
	make install && \
	cd /tmp && \
	rm ta-lib-0.4.0-src.tar.gz && \
	rm -r ta-lib
	
USER $NB_UID

RUN cd /tmp && \
    pip install jupyter_contrib_nbextensions -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    jupyter contrib nbextension install --user && \
    jupyter nbextension enable notify/notify && \
    jupyter nbextension enable codefolding/main && \
    jupyter nbextension enable hinterland/hinterland && \
    jupyter nbextension enable hide_input/main && \
    jupyter nbextension enable hide_input_all/main && \
    jupyter nbextension enable init_cell/main && \
    pip install ipywidgets -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install qgrid -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install matplotlib -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install seaborn -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install scikit-learn -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install ta-lib -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    jupyter nbextension enable --py qgrid && \
    jupyter nbextension enable --py widgetsnbextension && \
    rm -rf /home/$NB_USER/.cache

RUN cd /tmp && \
    wget --quiet https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda2-4.7.12.1-Linux-x86_64.sh && \
    /bin/bash Miniconda2-4.7.12.1-Linux-x86_64.sh -f -b -p /opt/conda2 && \
    rm Miniconda2-4.7.12.1-Linux-x86_64.sh && \
    /opt/conda2/bin/pip install notebook==5.6.0 -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    /opt/conda2/bin/pip install pandas -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    /opt/conda2/bin/pip install ipywidgets -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    /opt/conda2/bin/pip install qgrid -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    /opt/conda2/bin/pip install matplotlib -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    /opt/conda2/bin/pip install seaborn -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    /opt/conda2/bin/pip install scikit-learn -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
	/opt/conda2/bin/pip install ta-lib -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    /opt/conda2/bin/ipython kernel install --user --name python2 && \
    rm -rf /home/$NB_USER/.cache && \
    fix-permissions /opt/conda2 && \
    fix-permissions /home/$NB_USER