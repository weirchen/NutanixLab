.. _ssp:

-------------------
高級實作1：自助服務入口網站
-------------------

預計完成時間: 45分鐘
本實作使用Prism Central
在瀏覽器中打開Prism Central連結，使用admin使用者登錄Prism Central介面

實作目的
++++++++

在本練習中，您將會用到通過Prism Central來配置自助服務入口網站(SSP),並為不同的用戶組創建不同的專案。
該實作應該在進行Calm功能相關實作之前完成。

在Prism Central中設置身份驗證和角色映射
++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. note ::

  如果您已在Prism Central中配置了** Authentication **，請跳過此部分。
  
在 **Prism Central** 中，點擊 :fa:`cog` **>認證**

點擊 **+ New Directory**

#需根據實際實作環境修改
填寫以下欄位，然後按一下**Save**:

- **Directory Type** - AD活動目錄
- **Name** - NTNXLAB
- **Domain** - ntnxlab.local
- **Directory URL** - ldaps://10.21.XX.40 
- **Service Account Name** - administrator@ntnxlab.local
- **Service Account Password** - nutanix/4u

  .. figure:: images/ssp01.png

點擊黃色嘆號，緊連著**NTNXLAB**

  .. figure:: images/ssp28.png

點擊**點擊 Here** 進入到角色映射介面

點擊**+ New Mapping**

填寫以下欄位，然後按一下**Save**:

- **Directory** - NTNXLAB
- **LDAP Type** - user
- **Role** - Cluster Admin
- **Values** - administrator

  .. figure:: images/ssp29.png

關閉角色映射和身份驗證窗口

配置自助服務入口網站
+++++++++++++++++++++++++++++

.. note::

  如果已經在Prism Central配置了 **SSP**，請跳過此部分

我們將使用以下使用者資訊

+-----------------+-----------------------+--------------------------------+
| **Group**       | **Usernames**         | **Password**                   |
+-----------------+-----------------------+--------------------------------+
| SSP Admins      | adminuser01-20        | nutanix/4u                     |
+-----------------+-----------------------+--------------------------------+
| SSP Developers  | devuser01-20          | nutanix/4u                     |
+-----------------+-----------------------+--------------------------------+
| SSP Power Users | poweruser01-20        | nutanix/4u                     |
+-----------------+-----------------------+--------------------------------+
| SSP Basic Users | basicuser01-20        | nutanix/4u                     |
+-----------------+-----------------------+--------------------------------+

在**Prism Central**中, 點擊 :fa:`cog` **> Self-Service Admin Management**.

  .. figure:: images/ssp02.png

填寫以下欄位，然後按一下 **Next**:

- **Domain** - ntnxlab.local
- **Username** - administrator@ntnxlab.local
- **Password** - nutanix/4u

  .. figure:: images/ssp03.png

點擊 **+Add Admins**

  .. figure:: images/ssp04.png

輸入 **SSP Admins**, 並點擊 **Save**

  .. figure:: images/ssp05.png

點擊 **Save**

  .. figure:: images/ssp06.png

創建項目
+++++++++++++++

在本練習中，我們將創建3個項目。每個項目都將設置為不同的Active Directory組許可權。

在**Prism Central**中, 點擊 **Explore**

點擊 **Projects**

創建**Developers**項目
.............................

點擊 **Create Project**

填寫以下欄位:

- **Project Name** - Developers
- **Description** - SSP Developers
- **AHV Cluster** - *Assigned HPOC*

在**Users, Groups, and Roles**右下方，點擊藍色 **+User**連結

填寫以下欄位並點擊 **Save**:

- **NAME** - SSP Developers
- **ROLE** - Developer

  .. figure:: images/ssp08.png

 在**Network**中選擇適合的網路，並設置為預設
 
  .. figure:: images/ssp09.png

在**Quotas**選項前打勾

填寫以下欄位:

- **VCPUS** - 10 VCPUs
- **Storage** - 200 GiB
- **Memory** - 40 GiB

確認所有欄位元配置填寫完畢，然後點擊 **Save**

  .. figure:: images/ssp10.png

創建**Power Users**項目
..............................

點擊 **Create Project**

填寫以下欄位:

- **Project Name** - Power Users
- **Description** - SSP Power Users
- **AHV Cluster** - *Assigned HPOC*

在**Users, Groups, and Roles**右下方，點擊 **+User** 

填寫以下欄位並點擊 **Save**:

- **NAME** - SSP Power Users
- **ROLE** - Developer

在**Network**中選擇適合的網路，並設置為預設

在**Quotas**選項前打勾

填寫以下欄位:

- **VCPUS** - 10 VCPUs
- **Storage** - 200 GiB
- **Memory** - 40 GiB

確認所有欄位元配置填寫完畢，然後點擊 **Save**

  .. figure:: images/ssp11.png

創建**Calm**專案（如需要選做Calm實作的話）
.......................

點擊 **Create Project**

填寫以下欄位:

- **Project Name** - Calm
- **Description** - Calm
- **AHV Cluster** - *Assigned HPOC*

在**Users, Groups, and Roles**右下方，點擊 **+User** 

填寫以下欄位並點擊 **Save**:

- **NAME** - SSP Admins
- **ROLE** - Project Admin

填寫以下欄位並點擊 **Save**:

- **NAME** - SSP Developers
- **ROLE** - Developer

填寫以下欄位並點擊 **Save**:

- **NAME** - SSP Power Users
- **ROLE** - Consumer

填寫以下欄位並點擊 **Save**:

- **NAME** - SSP Basic Users
- **ROLE** - Operator

在**Network**中選擇適合的網路，並設置為預設

確認所有欄位元配置填寫完畢，然後點擊 **Save**

  .. figure:: images/ssp12.png

使用自助服務入口網站
+++++++++++++++++++++++

在本練習中，我們將以不同AD組的不同用戶身份登錄Prism Central。然後我們可以比較一下我們在SSP中看到的介面的區別，以及我們可以在不同許可權下做什麼操作。

我們先在Prism Central中登出現有管理員帳戶

使用SSP Admin角色登錄自助服務入口網站
......................................

使用以下憑據登錄Prism Central：

- **Username** - adminuserXX@ntnxlab.local (replace XX with 01-05)
- **Password** - nutanix/4u

  .. figure:: images/ssp13.png

登錄後，在頂部功能區中只有兩個選項卡， **Explore**和**Apps**

在**Explore**介面中點擊查看**VMs**, 您應該能看到**adminuserXX**對所有VM擁有存取工具

點擊**Projects**,您可以看到**adminuserXX**所屬的所有項目列表

  .. figure:: images/ssp14.png

現在讓我們在**Catalog**中增加一些映像檔, 點擊 **Images**

  .. figure:: images/ssp15.png

選擇**Windows2012**, 然後在**Actions**下拉式功能表中點擊 **Add Image to Catalog**

  .. figure:: images/ssp16.png

填寫以下欄位並點擊 **Save**:

- **NAME** - Windows2012 Image
- **Description** - Windows2012 Image

  .. figure:: images/ssp17.png

對CentOS映射重複這些步驟

點擊**Catalog Items**, 您將看到剛剛添加的兩個映像檔文件：

- CentOS Image
- Windows2012 Image

  .. figure:: images/ssp18.png

使用Developer角色登錄自助服務入口網站
......................................

使用以下憑據登錄Prism Central：

- **Username** - devuserXX@ntnxlab.local (replace XX with 01-05)
- **Password** - nutanix/4u

  .. figure:: images/ssp19.png

登錄後，在頂部功能區中只有兩個選項卡， **Explore**和**Apps**

在**Explore**介面中點擊查看**VMs**, 您應該能看到**devuserXX**對所有VM擁有存取工具

點擊**Projects**,您可以看到**devuserXX**所屬的所有項目列表


  .. figure:: images/ssp20.png

點擊**VMs**,然後點擊 **Create VM**

確認勾選了**Disk Images**, 然後點擊 **Next**

  .. figure:: images/ssp21.png

選擇**CentOS Image**,並點擊 **Next**

  .. figure:: images/ssp22.png

填寫以下欄位並點擊 **Save**:

- **Name** - Developer VM 001
- **Target Project** - Developers
- **Disks** - Select **Boot From**
- **Network** - Select **Primary**
- **Advance Settings** - Check **Manually Configure CPU & Memory**
- **CPU** - 1 VCPU
- **Memory** - 2 GB

  .. figure:: images/ssp23.png

您應該可以看到在VM列表中存在**Developer VM 001**

讓我們看看當我們以不同組的用戶身份登錄時會發生什麼

使用Power User角色存取自助服務入口網站
.......................................

使用以下憑據登錄Prism Central：

- **Username** - poweruserXX@ntnxlab.local (replace XX with 01-05)
- **Password** - nutanix/4u

  .. figure:: images/ssp24.png

登錄後，在頂部功能區中只有兩個選項卡， **Explore**和**Apps**

在**Explore**介面中點擊查看**VMs**, 您應該能看到**poweruserXX**對所有VM擁有存取工具

請注意，您無法看到** Developer VM 001 **，這是因為** SSP Power Users **不是該項目的成員。

點擊 **Create VM**

確認已選中**Disk Images**, 並點擊 **Next**

  .. figure:: images/ssp21.png

選擇**CentOS Image**, 然後點擊 **Next**

  .. figure:: images/ssp22.png

填寫以下欄位並點擊 **Save**:

- **Name** - Calm VM 001
- **Target Project** - Calm
- **Disks** - Select **Boot From**
- **Network** - Select **Primary**
- **Advance Settings** - Check **Manually Configure CPU & Memory**
- **CPU** - 1 VCPU
- **Memory** - 2 GB

  .. figure:: images/ssp25.png

您應該可以看到在VM列表中存在**Calm VM 001**

登出，並用**devuserXX@ntnxlab.local**帳戶重新登陸

您應該可以同時看到**Developer VM 001**和**Calm VM 001**兩台虛擬機器，這是因為**SSP Developers**帳戶同時是兩個項目的成員

  .. figure:: images/ssp26.png

按一下** Projects **，您將看到** Developer VM 001 **的資源使用情況與** Developer **專案配額相對應。
  .. figure:: images/ssp27.png

小技巧
+++++++++++

-  Nutanix提供原生整合服務，為不同的群組分離資源，同時為他們提供使用這些資源的自助服務方法。

- 使用目錄組輕鬆將資源配置給不同的專案

- 通過配額，可以輕鬆分配成群組資源，以更好地管理群集資源或進行回收

