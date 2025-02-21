#  Linux and DevOps Training

## Package Management

### RPM Commands
- `rpm -ivh <package.rpm>` - Install an RPM package
- `rpm -Uvh <package.rpm>` - Upgrade an RPM package
- `rpm -qa` - List all installed RPM packages
- `rpm -qi <package>` - Show detailed information about a package
- `rpm -ql <package>` - List files installed by an RPM package
- `rpm -e <package>` - Remove an RPM package

### YUM Commands
- `yum list installed` - List installed packages
- `yum search <package>` - Search for a package
- `yum install <package>` - Install a package
- `yum remove <package>` - Remove a package
- `yum update` - Update all installed packages
- `yum groupinstall <group>` - Install a package group

## System Services
- `systemctl list-units --type=service` - List all active services
- `systemctl start <service>` - Start a service
- `systemctl stop <service>` - Stop a service
- `systemctl restart <service>` - Restart a service
- `systemctl enable <service>` - Enable a service at boot
- `systemctl disable <service>` - Disable a service at boot
- `journalctl -xe` - View logs for system services

## Networking
- `ip a` - Show IP addresses
- `ip r` - Show routing table
- `netstat -tulnp` - Show active network connections
- `ping <hostname>` - Test network connectivity
- `traceroute <hostname>` - Trace the route to a host
- `dig <hostname>` - Get DNS information
- `nslookup <hostname>` - Query DNS records

## Java and Maven

### Java Commands
- `java -version` - Check Java version
- `javac <file.java>` - Compile a Java program
- `java <file>` - Run a Java program
- `echo $JAVA_HOME` - Check JAVA_HOME environment variable

### Maven Commands
- `mvn -version` - Check Maven version
- `mvn clean` - Remove target directory
- `mvn compile` - Compile the project
- `mvn package` - Package the project into a JAR/WAR
- `mvn test` - Run tests
- `mvn install` - Install the package into the local repository
- `mvn deploy` - Deploy the package to a remote repository