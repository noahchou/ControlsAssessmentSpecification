1.1: 建立和维护详细的企业资产清单
=====================================

建立和维持一个准确、详细和最新的所有企业资产清单，其中包括：终端用户设备(包括便携式和移动式)、网络设备、非计算/物联网设备和服务器。确保库存记录了网络地址（如果是静态的）、硬件地址、机器名称、数据资产所有者、每个资产的部门，以及该资产是否已被批准连接到网络。对于移动终端用户设备，MDM类工具可以酌情支持这一过程。该清单包括物理、虚拟、远程连接到基础设施的资产，以及云环境中的资产。此外，它还包括定期连接到企业网络基础设施的资产，即使它们不在企业的控制之下。每两年或更频繁地审查和更新所有企业资产的库存。

.. list-table::
	:header-rows: 1

	* - Asset Type
	  - Security Function
	  - Implementation Groups
	* - Devices
	  - Identify
	  - 1, 2, 3

Dependencies
------------
* None

Inputs
-----------
#. :code:`GV1`: Detailed Enterprise Asset Inventory - The enterprise's list of current approved inventory to include all assests as outlined in the safeguard. This list is a mix of manual and tool-generated endpoints that includes information such as authorized, non-authorized, IP address, device type and any other information as defined by the enterprise.
#. Aggregate Enterprise Asset Inventory - The enterprise's list of all devices detected, manually or through automated scans, since the last update to :code:`GV1`. 
#. Date of last update to the Detailed Enterprise Asset Inventory

Assumptions
^^^^^^^^^^^
#. Devices belonging to the organization, but not connected to the organization’s network, require manual discovery in order to be included in the aggregate inventory.

Operations
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
