# Task 5

## Install Maven
```bash
sudo apt install maven
```

![Screenshot from 2025-03-22 11-05-56](https://github.com/user-attachments/assets/4a778788-2264-44fa-8f73-47840573dd8f)

## Fork the repo on github

![Screenshot from 2025-03-22 11-06-03](https://github.com/user-attachments/assets/fcede585-563d-4da5-8332-1fe7368c4d8c)

## Configure Jenkins
 - In Jenkins go to `configure jenkins` > `tools`
 - Locate JDK section
 - Uncheck `Install Automatically`
 - Name `Java 17`
 - Go to terminal and enter the command and get the java 17 path:

```bash
update-java-alternatives --list 
```

 - paste the java path in `JAVA_HOME`

![Screenshot from 2025-03-22 12-26-20](https://github.com/user-attachments/assets/a3cb0fd1-18f8-40ad-8ac5-51866f925752)

## Add the pipeline script and build the pipeline

![Screenshot from 2025-03-22 12-26-50](https://github.com/user-attachments/assets/56a4a6bf-7d0f-44f5-bae7-1c106b5cac31)

## Verify the console to see the actions 

![Screenshot from 2025-03-22 12-27-04](https://github.com/user-attachments/assets/d9e61da7-24ad-4258-9513-69996f4de9be)
