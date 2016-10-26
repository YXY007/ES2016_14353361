<h1>Distributed Operation Layer</h1>
<p>The distributed operation layer (DOL) is a software development framework to program parallel applications. The DOL allows to specify applications based on the Kahn process network model of computation and features a simulation engine based on SystemC. Moreover, the DOL provides an XML-based specification format to describe the implementation of a parallel application on a multi-processor systems, including binding and mapping.</p>
<h2>Environment(take Ubuntu for example)</h2>
<p>Input the following instructions to install the environment for DOL.</p>
	$	sudo apt-get update
    $	sudo apt-get install ant
    $ 	sudo apt-get install openjdk-7-jdk
    $	sudo apt-get install unzip

<p>If jdk7 cannot be installed, try to change the source. Here is the steps of source changing:</p>
<p>Backup source configuration file</p>
	$   sudo cp /etc/apt/sources.list /etc/apt/sources.list_backup

<p>  Replace the content with the following code(Aliyun)</p>
	deb http://mirrors.aliyun.com/ubuntu/ trusty main multiverse restricted universe
	deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main multiverse restricted universe
	deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main multiverse restricted universe
	deb http://mirrors.aliyun.com/ubuntu/ trusty-security main multiverse restricted universe
	deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main multiverse restricted universe
	deb-src http://mirrors.aliyun.com/ubuntu/ trusty main multiverse restricted universe
	deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main multiverse restricted universe
	deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main multiverse restricted universe
	deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main multiverse restricted universe
	deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main multiverse restricted universe

<p>  Save the file and update</p>
	$    sudo apt-get update

<p>After changing the source, maybe jdk7 still cannot be intalled. Try installing jdk8 instead.</p>
<h2>File Downloading</h2>
<p>Input instructions to download files</p>
    $    sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz
    $    sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip

<h2>Decompression</h2>
<p>Open a new folder</p>
    $	mkdir dol

<p>Decompress dolethz.zip into the new folder</p>
    $	unzip dol_ethz.zip -d dol

<p>Decompress systemc</p>
    $	tar -zxvf systemc-2.3.1.tgz

<h2>Compile systemc</h2>
<p>Navigate into systemc-2.3.1</p>
	$	cd systemc-2.3.1

<p>Open a new folder objdir</p>
	$	mkdir objdir

<p>Navigate into objdir</p>
	$	cd objdir

<p>Run configure</p>
	$	../configure CXX=g++ --disable-async-updates

<p>The result is as follow</p>
<img src="http://img.blog.csdn.net/20160927222420459"/>

<p>Compile the file</p>
	$	sudo make install

<p>After compiling, the file list is as follow</p>
	$ cd ..        $ ls

<img src="http://img.blog.csdn.net/20160927222625459"/>

<p>Check the current path</p>
	$	pwd


<h2>Compile dol</h2>
<p>Navigate into dol</p>
	$	cd ../dol

<p>Find the following words</p>
	<property name="systemc.inc" value="YYY/include"/>

<p>And then alter it as</p>
	<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>

<p>Here YYY is the path we get at the insturction pwd</p>
<p>Compile</p>
	$	ant -f build_zip.xml all

<h2>Run the first example</h2>
	$	cd build/bin/main
	$	ant -f runexample.xml -Dnumber=1

<p>And the result is as follow</p>
<img src="http://img.blog.csdn.net/20160927221422493"/>

<h2>Experimental experience</h2>
<p>The most difficult part of this experiment is to install jdk, as it has failed several times. But then I found that the main reason for the failure is that the source is foreign, which is banned being visited. So I changed the source into domestic one and jdk-8 could be installed sucessfully with Aliyun source.</p>
<p>After the environment is configured, the installation process went good.</p>