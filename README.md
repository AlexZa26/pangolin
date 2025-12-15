# Краткое руководство по установке

> Разверните свой собственный полностью автономный экземпляр Pangolin Community Edition


## Prerequisites

## Предварительные требования

Перед началом работы убедитесь, что у вас есть:

*****Linux-сервер с правами root и общедоступным IP-адресом

***Доменное имя**, указывающее на IP-адрес вашего сервера для панели мониторинга

***Адрес электронной почты** для получения сертификатов Let's Encrypt SSL и входа в систему администратора

***Откройте порты на брандмауэре** для 80 (TCP), 443 (TCP), 51820 (UDP) и 21820 (UDP для клиентов)




## DNS и сеть

Before installing Pangolin, ensure you've set up DNS for your domain(s) and opened the required port on your firewall. See our guide on [DNS & networking](/self-host/dns-and-networking) for more information.

## Процесс установки

<Steps>
  <Step title="Загрузить программу установки">
    Подключитесь к своему серверу по SSH и загрузите программу установки:

    curl -fsSL https://raw.githubusercontent.com/AlexZa26/pangolin/refs/heads/main/get-installer.sh | bash
   

    Программа установки поддерживает архитектуры AMD64 (x86\\_64) и ARM64.
  </Step>

  <Step title="Запустить программу установки">
    Запустите программу установки с правами суперпользователя:

    sudo ./installer
    
    Установщик помещает все файлы в текущий каталог. Перед запуском программы установки переместите ее в нужный каталог.
  </Step>

  <Step title="Настройка основных параметров">
    Программа установки предложит вам выполнить необходимые настройки.:

    * **оОсновной домен**: Введите свой корневой домен без поддоменов (например, `example.com`)
    * **Домен панели мониторинга**: Нажмите Enter, чтобы принять значение по умолчанию `pangolin.example.com` или введите пользовательский домен
    * **Let's Encrypt Email**: Укажите адрес электронной почты для получения SSL-сертификатов и входа в систему администратора
    * **Туннелирование**: \*\*: Выберите, следует ли устанавливать Gerbil для туннелируемых подключений (по умолчанию: да). Вы можете запустить Pangolin без туннелирования. Он будет функционировать как стандартный обратный прокси-сервер.
  </Step>

  <Step title="Настройка электронной почты (необязательно)">
    <Tip>
      Функция электронной почты необязательна и может быть добавлена позже.
    </Tip>

    Выберите, следует ли включать функцию электронной почты SMTP:

    * **По умолчанию**: \*\*: Нет (рекомендуется для начальной настройки)
    * **Если включено**: Вам понадобятся данные SMTP-сервера (хост, порт, имя пользователя, пароль)
  </Step>

  <Step title="Начать установку">
    Подтвердите, что вы хотите установить и запустить контейнеры:

    * Программа установки загрузит образы Docker (pangolin, gerbil, traefik)
    * Контейнеры будут запущены автоматически
    * Этот процесс занимает 2-3 минуты в зависимости от вашего интернет-соединения

    Вы увидите индикаторы выполнения при загрузке каждого контейнера.
  </Step>

  <Step title="Установка CrowdSec (необязательно)">
    Программа установки спросит, хотите ли вы установить CrowdSec для обеспечения дополнительной безопасности:

    * **По умолчанию**: Нет (рекомендуется для начальной установки)
    * ***Если включено**: Вам нужно подтвердить, что вы согласны управлять конфигурацией CrowdSec

    <Warning>
      CrowdSec усложняет работу и требует ручной настройки для обеспечения оптимальной безопасности. Включайте только в том случае, если вам удобно управлять ею.
    </Warning>

    <Info>
      При необходимости CrowdSec можно установить позже. Базовая установка обеспечивает достаточную безопасность для большинства случаев использования.
    </Info>
  </Step>
</Steps>

## Post-Installation Setup

Once installation completes successfully, you'll see:

```
Installation complete!

To complete the initial setup, please visit:
https://pangolin.example.com/auth/initial-setup
```

<Steps>
  <Step title="Access the dashboard">
    Navigate to the URL shown in the installer output:

    ```
    https://<your-dashboard-domain>/auth/initial-setup
    ```

    <Check>
      The dashboard should load with SSL certificate automatically configured. It might take a few minutes for the first cert to validate, so don't worry if the browser throws an insecure warning.
    </Check>
  </Step>

  <Step title="Create admin account">
    Complete the initial admin user setup:

    * Enter your admin email address
    * Set a strong password
    * Verify your email (if email is configured)

    <Warning>
      Use a strong, unique password for your admin account. This account has full system access.
    </Warning>
  </Step>

  <Step title="Create your first organization">
    After logging in:

    1. Enter organization name and description
    2. Click "Create Organization"

    <Check>
      You're now ready to start adding applications and configuring your reverse proxy!
    </Check>
  </Step>
</Steps>


---

> To find navigation and other pages in this documentation, fetch the llms.txt file at: https://docs.pangolin.net/llms.txt
