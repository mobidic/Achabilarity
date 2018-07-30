BootStrap: yum
OSVersion: 7
MirrorURL: http://mirror.centos.org/centos-%{OSVERSION}/%{OSVERSION}/os/$basearch/
Include: yum

%labels
  AUTHOR nicolas.soirat@etu.umontpellier.fr

%post
  echo "Updating CentOS and installing mandatory packages ..."
  yum -y update 
  yum group install -y "development tools"
  yum -y install  wget git zlib-devel which 
  #For GATK 
  yum -y install java-1.8.0-openjdk-devel 
  #For MPA 
  yum install -y bzip2-devel ncurses-devel readline-devel tk-devel gdbm-devel xz-devel expat-devel 
  mkdir /softwares
  echo "... Done !"
  #For Phenolyzer
  yum -y install perl-devel
  yum -y install perl-CPAN
  curl -L http://cpanmin.us | perl - App::cpanminus
  cpanm --force Bio::Perl
  cpanm Switch 
  cpanm Graph::Directed 
  cpanm --force Bio::OntologyIO 
  cpanm --force Excel::Writer::XLSX

  echo "Installing the lastest release of Python ..."
  yum -y install https://centos7.iuscommunity.org/ius-release.rpm
  yum -y install epel-release
  yum -y install python34
  yum -y install python34-devel
  yum -y install python34-setuptools
  echo "... Done !"
  echo "Installing pip3 ..."
  easy_install-3.4 pip
  pip3 install PyVCF
  echo "... Done !"

  echo "Insalling BCFtools ..."
  git clone git://github.com/samtools/htslib.git
  git clone git://github.com/samtools/bcftools.git
  cd bcftools 
  make
  mv bcftools /usr/local/bin
  cd ..
  rm -rf bcftools
  echo "... Done !"

  echo "Installing Cromwell ..."
  wget https://github.com/broadinstitute/cromwell/releases/download/31.1/cromwell-31.1.jar
  mv cromwell-31.1.jar /softwares 
  echo "... Done !"

  echo "Installing GATK4 ..."
  wget https://github.com/broadinstitute/gatk/releases/download/4.0.4.0/gatk-4.0.4.0.zip
  unzip gatk-4.0.4.0.zip -d /softwares/
  rm gatk-4.0.4.0.zip 
  echo "... Done !"

  echo "Installing MPA ..."
  git clone https://github.com/mobidic/MPA.git
  mv MPA /softwares
  echo "... Done !"

  echo "Installing Phenolyzer ..."
  git clone https://github.com/WGLab/phenolyzer
  mv phenolyzer /softwares
  echo "... Done !"

  echo "Installing Captain-Achab ..."
  git clone https://github.com/mobidic/Captain-ACHAB.git
  mv Captain-ACHAB /softwares
  echo "... Done !"

  echo "Importing Captain Achab wdl from GitHub ..."
  git clone https://github.com/mobidic/MobiDL
  mv MobiDL /softwares 
  sed -i -e "s/modules\//\/softwares\/MobiDL\/modules\//g" /softwares/MobiDL/captainAchab.wdl 
  echo ".. Done !"

  echo "Importing Crom-wellWrapped from GitHub ..."
  git clone https://github.com/mobidic/Crom-wellWrapped
  mv Crom-wellWrapped /softwares 
  echo "... Done !"

%runscript
  echo "Run Crom-wellWrapped with theses arguments : $*"
  exec /softwares/Crom-wellWrapped/cww.sh -e /softwares/cromwell-31.1.jar -w /softwares/MobiDL/captainAchab.wdl "$@"


%help
  Captain ACHAB is a simple and useful interface to analysis of WES data for molecular diagnosis. 
  This container has a wrapper for cromwell you can launch with :

  /PATH/TO/singularity run captainAchab.simg -i [yourinputfile]_inputs.json 
  
  More options : 
  -c | --conf <file.conf> : To add a conf file
  -o | --option <option.json> : To add an option file
  -v | --verbosity <1, 2, 3 or 4> : To set verbosity level (ERROR : 1 | WARNING : 2 | INFO [default] : 3 | DEBUG : 4)
  -h | --help : Print help message in terminal and close the script

  Be careful, you have to put all your input files (except json) in your input folder. You must have these following files : 
  - phenotype.txt
  - gene_for_pathology.txt
  - vcf file
  - Genome of reference
  - Databases for Annovar 
  - Custom xref 
