# Road to Certification Commands

- `readlink /bin/sh`: show which shell /bin/sh points to.
- `echo $BASH_VERSION`
- `echo $SHELL`
- `uname`: kernel's name
- `tee <text file name to b created>`: the thee command allows you to both save the output to a file and display it to STDOUT. Useful when you are installing software from the command line and wnat to see what is happening as well as keep a log file of the transacton for later review.
- `rpm -U package-name.rpm` : installs or upgrades the specified package
- `rpm vs yum`: <https://www.digitalocean.com/community/tutorials/package-management-basics-apt-yum-dnf-pkg> - Software is usually distributed in the form of packages, kept in repositories.
  - RPM es un administrador de paquetes para sistemas basados ​​en Linux, mientras que YUM es una utilidad de administrador de paquetes para distribuciones de Linux basadas en RPM. En otras palabras, YUM es un frontend (contenedor de alto nivel) para RPM. **yum** can download and install all required dependencies automatically, but rpm will tell you to install a list of dependencies, and then you have to manually install them. RPM Package Manager allows you to install, upgrade, delete, query and verify packages on RPM-based Linux systems. RPM files comes with the .rpm extension. The RPM package consists of an archive file, that contains libraries and dependencies for a specific package, that do not conflict with other packages installed on your system.
  - Yum is a free and open-source command-line package-management application for Linux operating systems that uses the RPM Package Manager. Yum is a front-end tool for rpm that automatically solves dependencies for packages. It installs RPM software packages from distribution official repositories and other third-party repositories. Yum allows you to install, update, search and remove packages from your system.
  - Yum is a package manager and rpms are the actual packages. With yum you can add or remove software. The software itself comes within a rpm. The package manager allows you to install the software from hosted repositories and it will usually install dependencies as well.

| Operating System |    Format   |            Tool(s)            |
|:----------------:|:-----------:|:-----------------------------:|
| Debian           | .deb        | apt, apt-cache, apt-get, dpkg |
| Ubuntu           | .deb        | apt, apt-cache, apt-get, dpkg |
| CentOS           | .rpm        | yum                           |
| Fedora           | .rpm        | dnf                           |
| FreeBSD          | Ports, .txz | make, pkg                     |

- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- 