
Q-Factor Framework:

There are several components in the Q-Factor framework: 

  * a component that adds INT headers to outgoing packets at the source DTN  
  * a component that extracts telemetry metadata from incoming packets at the destination DTN  
  * the Telemetry Agent that processes telemetry metadata at the destination  
  
Adding INT headers to outgoing packets will follow these approaches:

  * the programmable NIC will add an INT header between the TCP header and user data. This approach requires special NICs at the source DTN but it uses no DTN's CPU, being completely transparent to the DTN operator.
  * an eBPF Traffic Control (tc) hook will be added to the end of the egress pipeline of Linux network stack. This approach requires no special hardware but implies in installing a new code in the source DTN.
  
Extracting telemetry metadata will follow these approaches:

  * the programmable NIC will remove the telemetry metadata between the TCP header and user data. This approach requires special NICs at the destination DTN but it uses no DTN's CPU, being completely transparent to the DTN operator.
  * an eBPF eXpress Data Path (XDP) hook will be added before the Linux network stack. This approach requires no special hardware but implies in installing a new code in the destination DTN.
  
Processing telemetry metadata by the Telemetry Agent will follow these approaches:

  * The Collector module will receive the telemetry metadata from the XDP hook or programmable NIC. The telemetry metadata will be parsed and submitted the Tuning module.
  * The Tuning module will process the telemetry metadata and make recommendations. These recommendations can be applied to the DTN or sent to the DTN's operator
  * The Telemetry Agent's API will enable operator to dynamically change the workflow, see the recommendations and tuning made, and export data to Network Monitoring Systems.
  
Each of the bullets above will have its own blueprint/user stories documented in the folder user-stories.