![image](https://github.com/user-attachments/assets/e12e92bc-1691-49a1-af6c-b74194753369)- University: [ITMO University](https://itmo.ru/ru/)
- Faculty: [FICT](https://fict.itmo.ru)
- Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
- Year: 2024/2025
- Group: K4112s
- Author: Osadchuk Elena Evgenyevna
- Lab: Lab3
- Date of create: 15.01.2025
- Date of finished: 15.01.2025

1. Запускаем Minikube.
2. Включаем Ingress (Включается поддержка Ingress-контроллера в Minikube)

![image](https://github.com/user-attachments/assets/f2ec1dab-b154-4d64-b191-8b5d3385bdb0)

3. Генерируем сертификат и ключ с помощью OpenSSL (Генерируется самоподписанный TLS-сертификат для моего FQDN)
В команде:
- openssl
Утилита для работы с криптографическими операциями, такими как генерация ключей, создание сертификатов и шифрование данных.
- req
Подкоманда req используется для работы с запросами на сертификаты (Certificate Signing Request, CSR) или для создания самоподписанных сертификатов.
- -x509
Указывает, что нужно создать самоподписанный сертификат X.509, а не CSR. X.509 — это стандарт для цифровых сертификатов, который используется в TLS/SSL.
- -nodes
Указывает, что приватный ключ не нужно шифровать (не использовать пароль). Это упрощает использование ключа в автоматизированных системах, так как нет необходимости вводить пароль каждый раз.
- -days 365
Указывает срок действия сертификата в днях. В данном случае сертификат будет действовать 365 дней.
- -newkey rsa:2048
Комбинирует две операции: Генерацию нового ключа и Использование алгоритма RSA с длиной ключа 2048 бит. RSA — это алгоритм асимметричного шифрования, широко используемый для создания TLS-ключей.
- -keyout tls.key
Указывает, что приватный ключ нужно сохранить в файл tls.key.
- -out tls.crt
Указывает, что сгенерированный сертификат нужно сохранить в файл tls.crt.
- -subj "/CN=front-fqdn.com/O=osadchuk_company"
Задает информацию для полей сертификата. Флаг -subj позволяет указать эту информацию без интерактивного ввода. /CN= front -fqdn.com: Указывает имя общего домена (Common Name, CN), для которого создается сертификат. /O= osadchuk_company: Указывает организацию (Organization, O), которая выпускает сертификат.

![image](https://github.com/user-attachments/assets/b94b2e6a-fa68-41ca-b63b-7eaf27b64262)

4. Создаем секрет для хранения сертификата (TLS-сертификат и ключ сохраняются в Kubernetes в виде секрета)

![image](https://github.com/user-attachments/assets/02e4e0c5-3bf0-4d49-888a-7a1f9c6f1a93)

5. Создаем и применяем YAML файл manifest.yaml (в файле создаю сразу все объекты: ConfigMap, ReplicaSet, Service и Ingress)

![image](https://github.com/user-attachments/assets/cad8821a-36a1-4df5-9c2a-85e2d6130774)
![image](https://github.com/user-attachments/assets/3eae893d-8cf7-4733-8951-6c3cf2cce96c)
![image](https://github.com/user-attachments/assets/4eeaa82b-5a66-4777-a2fe-990b1baecab2)

6. Добавляем запись в файл hosts

![image](https://github.com/user-attachments/assets/64eae278-ec56-4a97-b8b2-73cd819d9497)
![image](https://github.com/user-attachments/assets/e3909789-755c-47ad-92d5-7c8d59c35756)

7. Запускаем туннель Minikube (Minikube перенаправляет локальные запросы к вашему Ingress через туннель)

![image](https://github.com/user-attachments/assets/9c824001-3d41-4227-902a-650b89c15ff1)

8. Открываем браузер и переходим по адресу https://front-fqdn.com.

![image](https://github.com/user-attachments/assets/9457456a-b55a-41b5-8a5d-20b56c05531b)
![image](https://github.com/user-attachments/assets/0d20e3de-6b67-4ed9-ae65-8d20a8c7090d)

9. Нажимаем на замок рядом с адресом, чтобы увидеть информацию о сертификате

![image](https://github.com/user-attachments/assets/6cdd2142-db8f-4ace-9cbd-0d20c46b7670)

10. Схема организации

![image](https://github.com/user-attachments/assets/e2ef8cb6-9dd3-47e5-91f9-5ccb7f12ef32)
