- University: [ITMO University](https://itmo.ru/ru/)
- Faculty: [FICT](https://fict.itmo.ru)
- Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
- Year: 2024/2025
- Group: K4112s
- Author: Osadchuk Elena Evgenyevna
- Lab: Lab1
- Date of create: 08.01.2025
- Date of finished: 08.01.2025

1. Docker уже был установлен на компьютере, его нужно запустить, чтобы Minikube развернул кластер в изолированной среде.
2. Minikube устанавливаю по инструкции и после установки запускаю, тем самым создавая локальный кластер Kubernetes.

![image](https://github.com/user-attachments/assets/ea353507-c236-4afe-9ce7-ad3f21a19c66)

3. Затем подтягиваю kubectl, позволяющий выполнять команды для кластеров Kubernetes.

![image](https://github.com/user-attachments/assets/6ef63e95-ab05-47ec-84f5-44fe8a5a3371)

4. На рабочем столе создаю файл манифеста и в нем описываю pod и service.

![image](https://github.com/user-attachments/assets/8f35b2af-cbd5-4079-bc40-ea8a83287ec9)

5. В этом манифесте прописано, что Pod vault запускает контейнер с образом hashicorp/vault:latest, слушающий порт 8200;
Service vault обеспечивает доступ к этому Pod-у через порт 8200 внутри кластера и через порт 30080 снаружи кластера;
Подключение между Service и Pod обеспечивается с помощью метки app: vault.
6. Теперь применяю конфигурацию, указанную в манифесте к кластеру, тем самым создавая описанные ресурсы.

![image](https://github.com/user-attachments/assets/e43be889-ed57-4773-9d6e-3fe5bd7f89aa)

7. После этого пробрасываю порт сервиса кластера наружу (на локальную машину).

![image](https://github.com/user-attachments/assets/adcaba48-cdce-4164-92e1-b1cc04f6c4e5)

8. Ищу токен, необходимый для входа в хранилище, в логах Pod-а.

![image](https://github.com/user-attachments/assets/4b0d7898-0d74-4b0d-aaa7-874e3fc6e919)
![image](https://github.com/user-attachments/assets/b322f604-b359-40ee-839a-25c23e030a34)

9. Перехожу по адресу http://localhost:8200 на локальной машине и ввожу Root Token в соответствующее поле.
10. Теперь получаю доступ к хранилищу.

![image](https://github.com/user-attachments/assets/9628e12f-09ef-4bd5-95e4-82142f04ae10)

11. Схема организации контейнеров и сервисов в кластере выглядит следующим образом:

![image](https://github.com/user-attachments/assets/620ae4e3-2772-4e88-a083-e7efd85552f1)
