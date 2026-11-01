# High-Performance Deep Packet Inspection (DPI) Engine

A multi-threaded, high-performance Deep Packet Inspection (DPI) and traffic analysis engine implemented in modern C++. Designed for high-throughput packet processing, flow reassembly, SNI domain extraction, and customizable rule-based packet filtering from live network interfaces or offline PCAP capture files.

---

## Key Features

- **Multi-Threaded Architecture**: Scalable packet parsing using a lock-free/thread-safe queue and dedicated worker threads.
- **Fast Path Processing**: High-speed lookup and bypass pipeline for known safe/tracked traffic streams to maximize throughput.
- **Stateful Connection Tracking**: Tracks active TCP/UDP bidirectional sessions and connection states.
- **SNI Extractor**: Inspects TLS Client Hello handshakes to extract domain names (Server Name Indication) without decrypting payloads.
- **Rule Management**: Dynamic rule definition engine to inspect, flag, and filter traffic based on IP, port, protocol, or payload signatures.
- **Offline PCAP Analysis**: Native support for reading, parsing, and validating `.pcap` capture dumps.

---

## Project Structure

```text
├── include/
│   ├── connection_tracker.h   # Tracks bidirectional TCP/UDP flow states
│   ├── dpi_engine.h           # Core DPI engine orchestration
│   ├── fast_path.h            # Fast-path cache and accelerated processing
│   ├── load_balancer.h        # Distributes flow queues across worker threads
│   ├── packet_parser.h        # L2-L4 protocol decoding headers
│   ├── pcap_reader.h          # PCAP capture ingestion interface
│   ├── platform.h             # Cross-platform socket/network utilities
│   ├── rule_manager.h         # Signature matching and inspection rules
│   ├── sni_extractor.h        # TLS handshake SNI parsing logic
│   ├── thread_safe_queue.h    # Concurrent queue implementation
│   └── types.h                # Core data structures and typedefs
├── src/                       # Implementation files (.cpp)
├── CMakeLists.txt             # Build configuration
├── generate_test_pcap.py      # Python utility to synthesize test PCAP dumps
├── test_dpi.pcap              # Sample PCAP test file
└── README.md
