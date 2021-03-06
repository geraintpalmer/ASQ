.. _server-schedules:

=================================
Assign Work Schedules for Servers
=================================

ASQ allows users to assign cyclic work schedules to servers at each service centre.
An example cyclic work schedule may look like this:

	+-------------------+---------+---------+---------+---------+---------+---------+
	|    Shift Times    |    0-40 |  40-100 | 100-120 | 120-180 | 180-220 | 220-250 |
	+-------------------+---------+---------+---------+---------+---------+---------+
	| Number of Servers |       2 |       3 |       1 |       2 |       4 |       0 | 
	+-------------------+---------+---------+---------+---------+---------+---------+

This schedule is cyclic, therefore after the last shift (220-250), schedule begins again with the shift (0-40). The cycle length for this schedule is 250.

In order to define this work schedule, it must be given a name.
Let's call it :code:`my_special_schedule_01`.

In the :code:`parameters.yml` file, under :code:`Number_of_servers`, for the given node enter the name of the schedule. The :code:`cycle_length` must also be given.
An example is shown::

    cycle_length: 250
    Number_of_servers:
      - 'my_special_schedule_01'
      - 3

The equivalent way to add this to the parameters dictionary is by first adding the cycle length::
    
    'cycle_length':250

And then under number of servers, add the schedule name::

    'Number_of_servers':['my_special_schedule_01', 3]

This tells ASQ that at Node 1 the number of servers will vary over time according to the work schedule :code:`my_special_schedule_01`.
This schedule hasn't been defined yet.
To define the work schedule, add the following lines to the end of the :code:`parameters.yml` file::

    my_special_schedule_01:
      - - 0
        - 2
      - - 40
        - 3
      - - 100
        - 1
      - - 120
        - 2
      - - 180
        - 4
      - - 220
        - 0

And equivalently, adding the following to the parameters dictionary::

    'my_special_schedule_01':[[0, 2], [40, 3], [100, 1], [120, 2], [180, 4], [220, 0]]

Here we are saying that there will be 2 servers scheduled between times 0 and 40, 3 between 40 and 100, etc. The final shift denotes 0 servers between times 220 and :code:`cycle_length`, and then the schedule cycles to the beginning.
This fully defines the cyclic work schedule.

Note:

- If more than one work schedule is defined, the same :code:`cycle_length` must be used for the entire system.