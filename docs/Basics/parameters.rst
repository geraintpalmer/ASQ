.. _parameters-file:

===================
The Parameters File
===================

ASQ features a :code:`load_parameters` function that imports a parameters file as a dictionary. This file take is in :code:`.yml` format. A :code:`parameters.yml` file of this same format is required for use with :ref:`command-line-tool`.

A full example of the parameters file for a three node network with two classes of customer is shown below::

    Arrival_rates:
      Class 0:
      - 6.0
      - 4.5
      - 2.0
      Class 1:
      - 1.0
      - 1.8
      - 7.25
    detect_deadlock: False
    Number_of_classes: 2
    Number_of_nodes: 3
    Number_of_servers:
    - 2
    - 1
    - 1
    Queue_capacities:
    - "Inf"
    - "Inf"
    - 10
    Service_rates:
      Class 0:
      - - Exponential
        - 7.0
      - - Exponential
        - 5.0
      - - Gamma
        - 0.4
        - 0.6
      Class 1:
      - - Exponential
        - 8.5
      - - Triangular
        - 0.1
        - 0.8
        - 0.95
      - - Exponential
        - 3.0
    Simulation_time: 2500
    Transition_matrices:
      Class 0:
      - - 0.1
        - 0.6
        - 0.2
      - - 0.0
        - 0.5
        - 0.5
      - - 0.3
        - 0.1
        - 0.1
      Class 1:
      - - 0.7
        - 0.05
        - 0.05
      - - 0.5
        - 0.1
        - 0.4
      - - 0.2
        - 0.2
        - 0.2

The variable names are identical to the keys of the parameters dictionary (:ref:`parameters-dict`), and the keyword arguments that may also be used.