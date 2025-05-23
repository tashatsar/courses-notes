# [Курс по Docker и Kubernetes](https://stepik.org/course/99188/)🐳📦

## Контейнеры и Docker📦

Зачем нужны контейнеры? Перевозим крокодила, медоеда, гепарда и антилопу на одной барже:
- изоляция процессов
- портативность приложений
- масштабирование
- легковесность по сравнению с ВМ

🚮**Контейнер** — это легковесный, исполняемый пакет с приложением.

📦**Docker** — одна из систем для контейнеризации приложений. В докере есть:
- Контейнер (Container) - исполняемый пакет с приложением, подобен запущенной мини-виртуальной машине с изолированным внутри приложением
- Образ (Image) - это шаблон для запуска такой "машины"

Собрать образ `docker build . -t py_app:v0.1`

Список всех образов `docker images`

Запуск контейнера на основе образа `docker run py_app:v0.1`

Список запущенных контейнеров `docker ps`

Остановить определенный контейнер `docker stop 03f964310373`

Собирай но помни:
- MultiStage сборка Образов👣
- Минимизируйте количество слоев (`FROM`, `RUN`, `COPY` , `ADD` `&&`)🧅
- Держите статичные слои как можно выше⬆️

## Kubernetes🎺🥁📯🎶

Kubernetes (K8s) — это оркестратор, система для управления Контейнерами, упрощает взаимодействие с Нодами (серверами) и Подами (приложениями). В составе Пода может быть несколько Контейнеров.

**Проблемы Kubernetes**

**Эфемерность Подов** — Поды временны и могут перезапускаться (пересоздаваться) или перемещаться на другие Ноды. Для stateless-приложений это ок, для stateful-приложений нужно хранилище данных и механизмы восстановления состояния.

**Ресурсоемкость** — ВМ для Нод, подсистемы для управления, балансировки и хранения данных, Контейнеры с приложениями... Для 50 микросервисов это ок, для 10 -- будет достаточно и Docker Compose.

**Сложность** — высокий порог вхождения

### Архитектура кластера Kubernetes🏛️🏗️👷🏻‍♀️

_Kubernetes — это 5 бинарей (с):_
- kube-api-server
- kube-scheduler
- kube-controller-manager
- kubelet
- kube-proxy

Архитектура🏛️:
- Уровень **Control Plane** (управление состоянием кластера)
  - kube-api-server (обработка всех команд: пользователей, внутренних компонентов, от утилиты `kubectl`)
  - kube-scheduler (анализ ресурсов Нод и выбор подходящих для запуска Подов согласно критериям: кол-во памяти и ядер)
  - kube-controller-manager (управление контроллерами через взаимодействие с API)
  - etcd (key-value хранилище со всей инфомацией о состоянии кластера: кластер можно восстановить, имея резервную копию etcd. etcd не часть Kubernetes)
- Уровень **Data Plane** (работа приложений на воркер-нодах)
  - kubelet (агент на каждой Воркер Ноде, который отвечает за управление Подами)
  - kube-proxy (управление сетевым трафиком внутри кластера)
  - Runtime (среда выполнения контейнеров)

**Объекты/ресурсы в Kubernetes⚙️:**
- Namespace (Linux namespace, не K8s📁)
- Pod (набор из Контейнеров🫛)
- ReplicaSet
- Deployment

Внутри Namespace находятся Pods, внутри Pods находятся Containers, внутри Containers... а Ноды где? Поды в одном Неймспейсе могут быть с разных Нод, но Контейнеры в одном Поде только на одной Ноде.

### Контроллеры 

Контроллеры приводят текущее состояние к желаемому

#### Deployment

Deployment не контролирует Поды, Deployment -- контроллер контроллера ReplicaSet

Deployment➡️ReplicaSet➡️Pod1, Pod2, Pod3, etc

#### ReplicaSet

ReplicaSet поддерживает желаемое количество реплик 

**Deployment = функционал ReplicaSet + доп возможности**

| ReplicaSet    |Deployment |
| -------- | ------- |
| контролирует количество Подов  |контролирует ReplicaSet'ы |
| нет истории |создает ReplicaSet'ы и хранит историю релизов |
| нет откатов |позволяет делать откаты (благодаря истории релизов) |
|не поддерживает обновления |поддерживает обновления и позволяет настраивать стратегии обновления |

**ReplicaSet контролирует количество Подов
Deployment контролирует ReplicaSet'ы**

#### DaemonSet
Применяется редко, в основном если необходимо:
- задеплоить по одному Поду на каждую Ноду кластера. Обычно это связано с инфраструктурными кейсами, так, например, DaemonSet node-exporter устанавливает на каждую Ноду кластера Под, который собирает метрики с этой Ноды. Эти метрики передаются в Prometheus или Victoria Metrics. Затем по полученным метрикам можно строить дашборды в Grafana и настраивать на них алерты. 
- собирать логи с каждой Ноды (проекты: vector, fluentd), или настроить пинговалки между Нодами (k8s-pinger)
- настроить Ingress Nginx — балансировщик нагрузки для трафика, приходящего в кластер извне (схема имеет несколько недостатков)

#### Job
**Job** — это контроллер, который запускает Pod для выполнения конкретной задачи, а затем завершает его работу

Возможно, Вам доведется использовать Job, чтобы выполнять такие разовые задачи, как миграции БД.

#### CronJob

CronJob — это контроллер контроллера Job. CronJob запускает Job по расписанию, подобно cron в Linux. Это полезно для регулярных задач, таких как резервное копирование данных (например бэкап Postgres), отправка уведомлений или выполнение периодических вычислений.
