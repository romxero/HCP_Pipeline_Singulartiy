Bootstrap: shub
From: pndni/centos7-base:1.2.0
#OSVersion: 7
#MirrorURL: http://mirror.centos.org/centos-%{OSVERSION}/%{OSVERSION}/os/x86_64/
#Include: yum

%post

    ##############
    # freesurfer #
    ##############
    wget --no-verbose --output-document=/root/freesurfer.tar.gz https://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/6.0.1/freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.1.tar.gz
    tar -C /opt -xzvf /root/freesurfer.tar.gz
    rm /root/freesurfer.tar.gz

    #######
    # fsl #
    #######
    wget --output-document=/root/fslinstaller.py https://fsl.fmrib.ox.ac.uk/fsldownloads/fslinstaller.py 
    python /root/fslinstaller.py -p -V 6.0.1 -d /opt/fsl
    rm /root/fslinstaller.py

	##########
	# Connectome
	##########
	wget -O /root/workbench-rh_linux64-v1.3.2.zip https://www.humanconnectome.org/storage/app/media/workbench/workbench-rh_linux64-v1.3.2.zip
	unzip /root/workbench-rh_linux64-v1.3.2.zip -d /opt
	rm /root/workbench-rh_linux64-v1.3.2.zip -d 
	
	######
	#
	######
	wget -O /root/wu_gw_1.1.0.tar.gz https://github.com/Washington-University/gradunwarp/archive/v1.1.0.tar.gz
	tar -C /opt -zxvf /root/wu_gw_1.1.0.tar.gz 
	rm /root/wu_gw_1.1.0.tar.gz 
		
	######
	#
	######
	mkdir -p /opt/msm/bin
	wget -O /opt/msm/bin/msm_centos https://github.com/ecr05/MSM_HOCR/releases/download/1.0/msm_centos
