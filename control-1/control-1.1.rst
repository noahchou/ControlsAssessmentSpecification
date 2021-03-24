1.1: 建立和维护详细的企业资产清单
=====================================

建立和维持一个准确、详细和最新的所有企业资产清单，其中包括：终端用户设备(包括便携式和移动式)、网络设备、非计算/物联网设备和服务器。确保库存记录了网络地址（如果是静态的）、硬件地址、机器名称、数据资产所有者、每个资产的部门，以及该资产是否已被批准连接到网络。对于移动终端用户设备，MDM类工具可以酌情支持这一过程。该清单包括物理、虚拟、远程连接到基础设施的资产，以及云环境中的资产。此外，它还包括定期连接到企业网络基础设施的资产，即使它们不在企业的控制之下。每两年或更频繁地审查和更新所有企业资产的库存。

.. list-table::
	:header-rows: 1

	* - 資產類型
	  - 安全职能
	  - 执行小组
	* - 设备
	  - 识别
	  - 1, 2, 3

依赖性
------------
* None

輸入項田
-----------
#. :code:`GV1`: 详细的企业资产清单：企业当前核准的清单，包括保障措施中列出的所有资产。该清单是人工和工具生成的端点的组合，包括授权、非授权、IP 地址、设备类型等信息以及企业定义的任何其他信息。
#. 企业资产总清单：企业的所有设备清单，这些设备是自上次更新到 "企业资产总清单 "后，通过手动或自动扫描检测到的 :code:`GV1`. 
#. 企业资产详细清单的最后更新日期

假設條件
^^^^^^^^^^^
#. 屬於本組織但未連接到本組織網絡的設備，需要人工發現才能替換總清單。

運作方式
----------
#. Calculate the intersection of :code:`GV1` and Input 2
	#. Enumerate items in :code:`GV1` that are not in Input 2 (M4) 
	#. Enumerate items in Input 2 not in Input 1 (:code:`GV2`: M5). These assets are considered unauthorized. 
#. Check items in Input 1 for complete or missing detailed information
	#. Enumerate items that have complete information (M6)
	#. Enumerate items that do not have complete information or missing information (M7).
#. Calculate the time (in months) since the last update to Input 1 by using current date and Input 4 (M8).

Measures
--------
* M1 = :code:`GV1`
* M2 = Count of items in Input 2
* M3 = Count of items in the intersection of :code:`GV1` and Input 2
* M4 = Count of items in :code:`GV1` not found in Input 2
* M5 = :code:`GV2`
* M6 = Count of items in :code:`GV1` that contain all necessary detailed information
* M7 = Count of items in :code:`GV1` that do not contain detailed information
* M8 = Months since the last update to :code:`GV1`

Metrics
-------
* If M1 is not provided or available, then this safeguard is measured at a 0 and receives a failing score. The other metrics don't apply.
* If M8 is greater than six months, then this safeguard is measured at a 0 and receives a failing score. The other metrics don't apply.

Accuracy Score
^^^^^^^^^^^^^^^^^^^^^^^^^^
.. list-table::

	* - **Metric**
	  - | What percentage of the aggregate endpoint inventory is accounted for in the current enterprise asset inventory?
	* - **Calculation**
	  - :code:`M3 / M2`

Completeness Score
^^^^^^^^^^^^^^^^^^^^^^^^^^
.. list-table::

	* - **Metric**
	  - | What percentage of the current enterprise asset inventory contains necessary detailed information?
	* - **Calculation**
	  - :code:`M8 / M1`

Procedural Review
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Manual review/rating of the inventory procedures, to include adding and removing assets, and the time allowable or expected, after acquisition or disposal of assets.

.. history
.. authors
.. license
