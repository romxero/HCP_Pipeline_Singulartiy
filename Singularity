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
	# University of Washington Gradunwrap
	######
	wget -O /root/wu_gw_1.1.0.tar.gz https://github.com/Washington-University/gradunwarp/archive/v1.1.0.tar.gz
	tar -C /opt -zxvf /root/wu_gw_1.1.0.tar.gz 
	rm /root/wu_gw_1.1.0.tar.gz 
		
	######
	#MSM for Centos
	######
	mkdir -p /opt/msm/bin
	wget -O /opt/msm/bin/msm_centos https://github.com/ecr05/MSM_HOCR/releases/download/1.0/msm_centos

	######
	#FSL Fix
	######
	wget -O /root/fix.tar.gz http://www.fmrib.ox.ac.uk/~steve/ftp/fix.tar.gz
	tar -C /opt/fsl -zxvf /root/fix.tar.gz

%appenv freesurfer
    if [ -n "$FSLDIR" ]
    then
	>&2 echo "freesurfer must be loaded before fsl"
	exit 1
    fi
    export NO_FSFAST=1
    export FREESURFER_HOME=/opt/freesurfer
    source $FREESURFER_HOME/SetUpFreeSurfer.sh

%applabels freesurfer
    License https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferSoftwareLicense
    URL https://surfer.nmr.mgh.harvard.edu/
    Version 6.0.1

%apphelp freesurfer
    Using freesurfer requires a freesurfer license file.
    A license file may be obtained from
    https://surfer.nmr.mgh.harvard.edu/registration.html
    Ensure that the license file is visible from the container,
    and set the environment variable FS_LICENSE to point to it
    (or copy the file to /opt/freesurfer/license.txt from
    inside the container)

%appenv fsl
    export FSLDIR=/opt/fsl
    source $FSLDIR/etc/fslconf/fsl.sh
    export PATH=$FSLDIR/bin:$PATH

%appenv workbench
    export WKBLDIR=/opt/workbench/
    export PATH=$FSLDIR/bin_rh_linux64:$PATH

%appenv all
    source $SCIF_APPENV_freesurfer
    source $SCIF_APPENV_fsl
    source $SCIF_APPENV_workbench

%applabels fsl
    License https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/Licence
    URL https://fsl.fmrib.ox.ac.uk/fsl/fslwiki
    Version 6.0.1

%apphelp fsl
    Before using FSL you must agree to the license at
    https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/Licence

%labels
    Maintainer Steven Tilley
    Version 1.0.1

%apphelp all
    Set up environment for freesurfer and FSL

    Using freesurfer requires a freesurfer license file.
    A license file may be obtained from
    https://surfer.nmr.mgh.harvard.edu/registration.html
    Ensure that the license file is visible from the container,
    and set the environment variable FS_LICENSE to point to it
    (or copy the file to /opt/freesurfer/license.txt from
    inside the container)

    By using FSL you agree to the license at
    https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/Licence
