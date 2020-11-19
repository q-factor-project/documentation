
User Stories for the Linux hooks to add and extract telemetry metadata within the Linux kernel space.

  1. Outgoing packets should be expanded with an INT header specified in the INT Spec v1.0.
  2. Outgoing packets should be expanded with an INT header only when the remote node is a Q-Factor node
  3. Outgoing packets should be expanded with an INT header at the lowest point within the Linux network stack
  4. Outgoing packets when TCP with TCP Options are present, should add INT header between the TCP standard header and the TCP Options
  5. Outgoing packets will increase in 12 bytes, MTU needs to be mapped in advance to avoid drops
  6. Outgoing packets should be expanded with an INT header using Traffic Control (tc) available via iproute2
  7. Outgoing packets should be expanded with an INT header leveraging eBPF calls
  8. Outgoing packets should be marked with DSCP code AF17 following the INT Spec v1.0

  10. Incoming packets with an INT header should have the INT metadata extracted at the lowest point within the Linux network stack
  11. Incoming packets with an INT header should have the INT metadata extracted using eXpress Data Path (xdp)
  12. Incoming packets with an INT header should have the INT metadata pre-processed looking for possible anomalies to save context switching costs. The output of the pre-processing will be the telemetry summaries.
  13. All telemetry summaries should be pushed to the Telemetry Agent via eBPF maps, eBPF PERF calls, or a new packet (for Remote Telemetry Agents)

Challenges:

  * In INT-enabled networks, INT sinks can't extract the telemetry metadata from Q-Factor flows
  * Only communication between Q-Factor nodes should have INT headers added