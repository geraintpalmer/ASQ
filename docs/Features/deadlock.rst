.. _deadlock-detection:

=============================
Deadlock Detection Capability
=============================

ASQs has built in deadlock detection capability. With ASQ, a queueing network can be simulated until it reaches deadlock. ASQ then records the time until deadlock from each state.

In order to take advantage of this feature, set deadlock detection option to True in the parameters file::

    detect_deadlock: False

Then use the :code:`simulate_until_deadlock` method to return the times to deadlock from each state::

   >>> import asq
   >>> Q = asq.Simulation(deadlock_params)
   >>> times = Q.simulate_until_deadlock()

where :code:`times` is a dictionary with states as keys and times to deadlock as values. Note that :code:`Simulation_time` is ingnored in this case.



------------------
Example - Deadlock
------------------

Consider the M/M/1/3 queue where customers have probability 0.5 of rejoining the queue after service. If the queue is full then that customer gets blocked, and hence the system deadlocks.

Parameters::

    >>> params = {'Arrival_rates': {'Class 0': [6.0]},
    ...           'Number_of_nodes': 1,
    ...           'detect_deadlock': True,
    ...           'Simulation_time': 2500,
    ...           'Number_of_servers': [1],
    ...           'Queue_capacities': [3],
    ...           'Number_of_classes': 1,
    ...           'Service_rates': {'Class 0': [['Exponential', 5.0]]},
    ...           'Transition_matrices': {'Class 0': [[0.5]]}}

Running until deadlock::

    >>> import asq
    >>> seed(99)
    >>> Q = asq.Simulation(params)
    >>> times = Q.simulate_until_deadlock()
    >>> times
    {((1, 0),): 1.0845416939916719, ((3, 0),): 0.5436399978272065, ((0, 0),): 1.1707879982560288, ((4, 0),): 0.15650986183172932, ((3, 1),): 0.0, ((2, 0),): 1.0517097907100657}

Here the state :code:`((i, j),)` denotes the state where there are `i` customers at the node, `j` of which are blocked. 