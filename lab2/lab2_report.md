- University: [ITMO University](https://itmo.ru/ru/)
- Faculty: [FICT](https://fict.itmo.ru)
- Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
- Year: 2024/2025
- Group: K4112s
- Author: Osadchuk Elena Evgenyevna
- Lab: Lab2
- Date of create: 08.01.2025
- Date of finished: 08.01.2025

1. Как в 1 лабораторной запускаю Minikube.
2. Создаю новый манифест, описывая в нем deployment (указвая количество реплик и переменные окружения) и service.

   ![image](https://github.com/user-attachments/assets/27eaeae3-700c-4583-aa29-dfde99967104)

3. Применяю манифест, создавая описанные в нем ресурсы.
4. Пробрасываю порты наружу.

   ![image](https://github.com/user-attachments/assets/6c7b26df-334d-443b-9058-51fdcf5f3238)

5. Перехожу по адресу http://localhost:30080.

   ![image](https://github.com/user-attachments/assets/0e27b4a7-5043-4d9b-9027-9d22cfde9c53)

6. На странице в веб браузере отображаются переменные окружения и Container name. При перезагрузке страници ничего не меняется. Даже если пекратить прокидывание и начать заново, снова будет тот же Container name.
Я нашла следующую информацию, объясняющую это:

Во-первых, в официальной документации сказано, что команда port-forward пробрасывает локальные порты к портам Pod-а (одного конкретного) и, если у нас есть несколько Pod-ов удовлетворяющих критериям (то есть указанному порту), Pod выбирается автоматически.
  ![image](https://github.com/user-attachments/assets/82eb58a5-f3ff-4ee8-b762-e304a23bf683)

Во-вторых, в одной из статей я нашла подтверждение этому (тут сказано, что локальный порт пробрасывается через указанный targetPort сервиса на Pod, выбираемый сервисом)

  ![image](https://github.com/user-attachments/assets/b5569a38-c462-451d-af76-5f92dd09bbe3)

Чтобы этого избежать, нужно использовать другие команды, которые будут использовать балансировщик нагрузки.

7. Проверяем логи контейнеров.

   ![image](https://github.com/user-attachments/assets/07d7f69d-5073-4385-bef2-49741a04d6d6)

8. Схема организации контейнеров и сервисов в кластере выглядит следующим образом:

   ![k8s2](https://github.com/user-attachments/assets/145d11d5-c25d-4f22-8a38-cf3c742b1ee9)
