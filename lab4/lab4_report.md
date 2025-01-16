- University: [ITMO University](https://itmo.ru/ru/)
- Faculty: [FICT](https://fict.itmo.ru)
- Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
- Year: 2024/2025
- Group: K4112s
- Author: Osadchuk Elena Evgenyevna
- Lab: Lab4
- Date of create: 15.01.2025
- Date of finished: 15.01.2025

1. Установливаем Minikube с плагином CNI=calico и включаем режим Multi-Node Clusters
minikube start: Запускает кластер Minikube.
--nodes=2: Создает кластер с двумя нодами.
--cni=calico: Указывает, что нужно использовать плагин CNI (Container Network Interface) Calico. 

![image](https://github.com/user-attachments/assets/b0ccdb04-a3a5-431e-b0f2-ac03f6caa8e8)

2. Проверяем работу CNI Calico и количество нод
 
![image](https://github.com/user-attachments/assets/c27a9ca4-d729-4a9a-b052-8734073317d5)
![image](https://github.com/user-attachments/assets/e5fc7be3-e540-49e6-9e87-078db9360bb6)

3. Добавляем метки по стойке (rack) для нод

![image](https://github.com/user-attachments/assets/f78bfea5-b4f2-4040-8d88-3399108521c5)

4. Пишем новый манифест, где создаем Calico, Deployment и сервис, применяем манифест.
IPPool: Определяет пул IP-адресов для подов.
nodeSelector: Указывает, на какие ноды применять пул.
 
![image](https://github.com/user-attachments/assets/4df5495f-08fd-4082-9ccd-bec6f6015e1d)
![image](https://github.com/user-attachments/assets/b151a70e-a69b-4371-bcfb-482734a27abe)
![image](https://github.com/user-attachments/assets/e5973e88-89ff-47db-82a0-045e05a46515)

5. Включаем режим проброса портов

 ![image](https://github.com/user-attachments/assets/20e0f324-1475-452b-bbac-157d2fd244ea)
 ![image](https://github.com/user-attachments/assets/6bf68ea8-71cc-4333-865c-b35e2b2ba032)

6. Проверяем переменные и IP-адреса
Обновляем веб-приложение. Имя контейнера и IP-адрес контейнера изменяются, потому что каждый под (реплика) создается заново при пересоздании или обновлении.

 ![image](https://github.com/user-attachments/assets/28309877-06d0-46ca-98b8-702589d3fcf7)

7. Пинг подов, используя FQDN
svc — это сервис, который позволяет Kubernetes управлять доступом между подами.
cluster.local — стандартное доменное имя для всех подов в Kubernetes.

 ![image](https://github.com/user-attachments/assets/8e6cc669-2134-4f2e-8ac0-5b064d9eedc2)

8. Схема организации

   
