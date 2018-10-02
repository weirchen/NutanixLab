.. _lab_data_protection:

---------------------
中級實作5:資料保護與復原
---------------------
預計完成時間: \ **15分鐘**

本實作使用\ **Prism Element**

在瀏覽器中打開Prism Element連結，登錄Prism Element介面。


實作目的
++++++++

本實作主要學習如何設置保護域(Protection Domains)，創建VM快照以及從這些快照復原資料。

資料保護
+++++++++++++++

在Prism中，資料保護策略稱為保護域（PD）。

PD由一組VM和策略組成，可用策略包括快照，複製目標位置和日程計畫。

VM快照與復原
............

創建VM快照並從快照還原VM。

在**Prism Element> VM**中，按一下**VM**，然後按一下**Table**

找到您在上一個實作中創建的Linux VM（Linux_VM- *intials*）
 - 如果VM已開啟，請將其關閉

選擇VM，然後從VM清單下方的功能表中按一下 **Snapshot**。

.. figure:: images/data_protection01.png
 
為快照起一個名字(註：intials輸入實作人員的姓名全名的拼音）

.. figure:: images/data_protection02.png

點擊submit提交

返回VM列表並按一下VM的名稱以打開其控制台視窗

按一下**Snapshots**以查看快照

.. figure:: images/data_protection03.png

- 請注意此步驟還有四個可用操作(Details, Clone, Restore, and Delete)（詳細資訊，副本，還原和刪除）

.. figure:: images/data_protection04.png

按一下**Details**可查看快照時的所有VM屬性

現在我們可以通過刪除虛擬磁碟模擬我們的測試VM遭到損壞的情況

按一下VM下面功能表中的Power Off Actions,選擇Guest Shutdown關閉虛機

VM前面的綠點變為紅點後，按一下下面功能表中的**Update**並修改您拍攝快照的原始VM

.. figure:: images/data_protection05.png

向下滾動到虛擬磁碟部分，通過點擊**X**圖示，刪除CD-ROM和DISKS

點擊**Save**確認更改.

.. figure:: images/data_protection06.png


現在嘗試啟動該VM並打開其控制台視窗

 .. figure:: images/data_protection07.png

 - 注意，VM此時不再有任何可開機的虛擬磁碟，並且顯示2048遊戲。
 
 .. figure:: images/data_protection08.png


關閉VM電源。

選擇VM，然後從VM清單下方的功能表中按一下**VM Snapshots**.

點擊**Restore**將VM復原到刪除虛擬磁碟之前的狀態.

 .. figure:: images/data_protection09.png


嘗試打開VM並打開控制台。

驗證VM是否已成功開機以及其配置是否已還原

配置保護域（PD）
..................................

創建Async DR （資料非同步複寫）
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

在**Prism Element > Data Protection**中, 按一下**Data Protection**, 然後點擊**Table**.

選擇**+ Protection Domain** 以創建PD，然後按一下創建Async DR.

.. figure:: images/data_protection10.png

輸入PD的名稱PD-\ *NAME* （註： NAME輸入實作人員的姓名全名的拼音）

然後按一下**Create**.

選擇您希望加入PD的VM:

- 通過過濾或滾動以選擇您在此訓練營中創建的VM，加入到此PD中
- 向下滾動並按一下**Protect Selected Entities**.
- 所選VM顯示在右側表中，點擊**Next**.

 .. figure:: images/data_protection11.png


**配置日程計畫**:

- 按一下**New Schedule**.

-  選擇備份頻率(如,每兩小時做一次快照).

-  設置保留策略(比如, 保持最多12份快照).

-  按一下\ **Create Schedule**.

 .. figure:: images/data_protection12.png

-  一個保護域可以有多個計畫

-  點擊\ **Close**\ 退出.

 .. figure:: images/data_protection13.png

加入遠端站點
~~~~~~~~~~~~~~~~~~~~~~~

註：本地備份是此實作室環境中的唯一選項，沒有配置遠端目標，在有遠端站點的情況下，可以按一下\ **+Remote Site**\ 進行配置，遠端站點可以是Nutanix實體集群環境，或者是公有雲環境。
.. note::

  本地備份是此實作室環境中的唯一選項，因為未配置遠端目標。
  您可以使用鄰近群集設置遠端站點
  
按一下**Create Schedule**.

.. note::

  一個保護域可以有多個計畫
  
點擊**Close**退出.

 .. figure:: images/data_protection13.png


小技巧
+++++++++

 -  Nutanix通過不同的策略為虛擬資料中心提供資料保護解決方案，包括一對一或一對多複製。
 -  Nutanix在VM，檔案和卷冊組級別提供資料保護功能，因此VM和資料在崩潰一致的環境中保持安全。
 - 您可以通過Web控制台配置保護域和遠端站點來實施資料保護策略。

