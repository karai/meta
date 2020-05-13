# P2P Channel Connection Handshake Process
This is a living document describing the peer handshake process when joining a Karai transaction channel.

### Later additions & enhancements
- TRTL PKI
- QUIC

Rough flow of events:
- user finds ktx address.. 
- user uses `connect-channel <address>` format in karai client
- user's karai instance sends a GET request to the /version endpoint of the coordinator first. (the logic behind this is if we can't talk anyway, we should end the convo as soon as possible)
  - if coord version query fails to satisfy version required, disconnect, record ktx address and version info
  - if coord version query passes the client's requirements, the user sends their own version in a client-header to initiate handshake process 
- <if any authentication of a user in a private channel is required this is where someone would implement that.>
- the coordinator responds to the handshake request with the most current milestone tx transaction containing the current the governance parameters of the channel 
- user responds with ACK as a standard transaction in the channel announcing the completion of the handshake process 
- assuming the ACK is accepted, the coordinator broadcasts the join TX and the process is done.
