FROM jupyterhub/k8s-singleuser-sample:0.8.2

USER root

RUN cd /tmp && \
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
    pip install --upgrade pip -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install jupyter_contrib_nbextensions -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    jupyter contrib nbextension install --user && \
    jupyter nbextension enable notify/notify && \
    jupyter nbextension enable codefolding/main && \
    jupyter nbextension enable hinterland/hinterland && \
    jupyter nbextension enable hide_input/main && \
    jupyter nbextension enable hide_input_all/main && \
    jupyter nbextension enable init_cell/main && \
    pip install qgrid -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install matplotlib -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install seaborn -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install scikit-learn -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install ta-lib -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install xlrd -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install xlwt -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install tensorflow==2.3.1 --use-feature=2020-resolver -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    pip install Keras==2.4.3 --use-feature=2020-resolver -i http://pypi.douban.com/simple/  --trusted-host pypi.douban.com && \
    jupyter nbextension enable --py qgrid && \
    rm -rf /home/$NB_USER/.cache