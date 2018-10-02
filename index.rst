.. title:: Introduction to Nutanix AHV

.. toctree::
  :maxdepth: 2
  :caption: Nutanix技術概覽
  :name: _technology_overview
  :hidden:

  what_is_nutanix/what_is_nutanix
  nutanix_terminology/nutanix_terminology

.. toctree::
  :maxdepth: 2
  :caption: 初級實驗-初始配置
  :name: _nutanix_configuration_labs
  :hidden:

  lab_nutanix_tech_overview/lab_nutanix_tech_overview
  lab_storage_configuration/lab_storage_configuration
  lab_network_configuration/lab_network_configuration

.. toctree::
  :maxdepth: 2
  :caption: 初級實驗-AHV部署與管理
  :name: _deploying_and_managing_workloads
  :hidden:

  lab_deploy_workloads/lab_deploy_workloads
  lab_manage_workloads/lab_manage_workloads
  
.. toctree::
  :maxdepth: 2
  :caption: 中級實驗-資料保護與恢復
  :name: _monitoring_and_managing_the_environment
  :hidden:
  
  backup_and_dr/backup_and_dr
  lab_data_protection/lab_data_protection
  
.. toctree::
  :maxdepth: 2
  :caption: 中級實驗-集中監控和管理
  :name: _monitoring_and_managing_the_environment
  :hidden:

  monitoring_and_managing_env/monitoring_and_managing_env
  lab_monitoring_env/lab_monitoring_env
  

.. toctree::
  :maxdepth: 2
  :caption: 高級實驗-ssp
  :name: _optional_labs
  :hidden:

  ssp/ssp

.. toctree::
  :maxdepth: 2
  :caption: 高級實驗-Flow
  :name: _optional_labs
  :hidden:
  
  flow/flow
  
.. toctree::
  :maxdepth: 2
  :caption: 高級實驗-Calm
  :name: _optional_labs
  :hidden:
  
  calm/calm
  

.. toctree::
  :maxdepth: 2
  :caption: 附錄
  :name: _appendix
  :hidden:

  appendix/glossary
  appendix/basics

.. _前言:

---------------
前言
---------------

歡迎來到Nutanix Hands on Lab技術實作訓練營！本實驗手冊將與實驗講師的指導相配合，重點對Nutanix技術和許多常見的管理任務進行展示和介紹。每個章節都有對應的知識點介紹和動手練習，為您提供實踐練習。實驗講師將負責解釋並回答您可能在動手實驗中遇到的任何其他問題。

在訓練營結束時，與會者應該可以對Nutanix企業雲架構的基本概念和技術有所瞭解，並且能夠有能力進行現場或利用遠端環境進行POC或日常進行系統管理的能力。

更新日誌
++++++++++

- 動手實驗室環境已經針對以下軟體版本進行更新:
    - AOS 5.8
    - PC 5.8.1

- 高級實驗部分的動手實驗室更新:
    - SSP自助服務門戶
    - Flow軟體定義網路


實驗目錄
++++++

-
初級實驗1:NUTANIX管理介面介紹 
初級實驗2:儲存容器配置  
初級實驗3:網路配置  
初級實驗4:AHV的虛機部署與管理 
中級實驗5:資料保護與復原 
中級實驗6:監控與管理 
高級實驗7:自助服務路口網站
高級實驗8：FLOW網路虛擬化



實驗環境細節
+++++++++++++++++++

Nutanix實驗室將會在Nutanix HPOC或現場實驗環境中運行，實驗講師將為您的群集配置完成練習所需的所有必要映像檔，連接網路和VM。


網路環境
..........

託管POC集群環境的通用命名規則:

- **群集名稱** - POC\*XYZ*
- **子網** - 10.**21**.\*XYZ*\ .0
- **群集IP** - 10.**21**.\*XYZ*\ .37

例如:

- **群集名稱** - POC055
- **子網** - 10.21.55.0
- **群集IP** - 10.21.55.37

在動手實驗中，有多個實驗場景需要用*XYZ*替換子網的正確八位元位元組:

.. list-table::
   :widths: 25 75
   :header-rows: 1

   * - IP地址
     - 說明
   * - 10.21.\ **XYZ**\ .37
     - Nutanix群集虛擬IP
   * - 10.21.\ **XYZ**\ .39
     - **PC** VM IP, Prism Central
   * - 10.21.\ **XYZ**\ .40
     - **DC** VM IP, NTNXLAB.local 網域控制站

每個群集配置有2個VLAN，可用於VM:

.. list-table::
  :widths: 25 25 10 40
  :header-rows: 1

  * - Network Name
    - Address
      - VLAN
      - DHCP Scope
  * - 主地址
    - 10.21.\ *XYZ*\ .1/25
    - 0
    - 10.21.\ *XYZ*\ .50-10.21.\ *XYZ*\ .124
  * - 次地址
    - 10.21.\ *XYZ*\ .129/25
    - *XYZ1*
    - 10.21.\ *XYZ*\ .132-10.21.\ *XYZ*\ .253

密碼
...........

.. 注意::

  *<Cluster Password>* 對每個群集都是唯一的，將由Workshop的負責人提供

.. list-table::
   :widths: 25 35 40
   :header-rows: 1

   * - 密碼
     - Username
     - Password
   * - Prism Element
     - admin
     - *nx2Tech308!*
   * - Prism Central
     - admin
     - *nx2Tech308!*
   * - Controller VM
     - nutanix
     - *nx2Tech308!*
   * - Prism Central VM
     - nutanix
     - *nx2Tech308!*

每個群集都有一個專用的網域控制站VM，**DC**，負責為 **NTNXLAB.local** 域提供AD服務。該網域包含以下用戶和群組：


.. list-table::
   :widths: 25 35 40
   :header-rows: 1

   * - Group
     - Username(s)
     - Password
   * - Administrators
     - Administrator
     - nutanix/4u
   * - SSP Admins
     - adminuser01-adminuser32
     - nutanix/4u
   * - SSP Developers
     - devuser01-devuser32
     - nutanix/4u
   * - SSP Power Users
     - poweruser01-poweruser32
     - nutanix/4u
   * - SSP Basic Users
     - basicuser01-basicuser32
     - nutanix/4u

存取說明
+++++++++++++++++++

可以通過多種不同方式存取Nutanix Hosted POC環境:

1)Citrix XenDesktop桌面(推薦)
.................

https://citrixready.nutanix.com - *Accessible via the Citrix Receiver client or HTML5*

**Nutanix內部員工** - 使用Nutanix公司SSO域帳戶
**非Nutanix員工** - **用戶名:** POCxxx-User01 (up to POCxxx-User20), **密碼:** *<培訓講師提供>*

2)Employee Pulse Secure VPN
..........................

https://sslvpn.nutanix.com - 使用Nutanix域帳戶登陸

Non-Employee Pulse Secure VPN
..............................

https://lab-vpn.nutanix.com - **用戶名:** POCxxx-User01 (up to POCxxx-User20), **密碼:** *<培訓講師提供>*

在**Client Application Sessions**介面, 找到右下角的 **Pulse Secure** 圖示右側的**Start** 按鈕，下載用戶端。

下載並安裝**Pulse Secure**用戶端軟體.

按照如下資訊添加一個連接:

- **Type** - Policy Secure (UAC) or Connection Server
- **Name** - HPOC VPN
- **Server URL** - lab-vpn.nutanix.com


