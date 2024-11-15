# Security Log Tokenizer

A specialized tokenizer for security logs designed to improve cloud security log analysis and processing.

## Overview

This project implements a custom BytePair Encoding (BPE) tokenizer specifically trained on security logs. Unlike general-purpose tokenizers, this implementation is optimized for security-specific content including IP addresses, timestamps, process IDs, and other security-relevant information commonly found in cloud environments.

## Why It Matters for Cloud Security

### 1. Enhanced Log Processing
- **Efficient Parsing**: Better tokenization of security-specific terms and patterns
- **Improved Analysis**: More accurate processing of security logs from various cloud services
- **Format Support**: Handles diverse log formats from different cloud providers and services:
  - Azure Monitor logs
  - AWS CloudTrail
  - Cloud firewall logs
  - Authentication events
  - Network access logs

### 2. Security Applications
- **Anomaly Detection**: Better tokenization leads to improved anomaly detection in log analysis
- **Pattern Recognition**: Enhanced ability to identify security patterns and threats
- **Log Analysis**: More accurate processing for:
  - Authentication failures
  - Access control violations
  - Network security events
  - Configuration changes
  - Security alerts

## Features

- Custom BPE tokenizer trained specifically on security logs
- GPT-4 generated training data for diverse log formats
- Support for multiple log types:
  - Windows Event logs
  - Linux syslog entries
  - Firewall logs
  - Authentication logs
  - Network access logs
  - Web server logs
  - DNS query logs
  - Database access logs
- Persistent training data storage
- Rate-limited API calls with retry logic
- Comprehensive tokenizer testing

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/security-log-tokenizer.git
cd security-log-tokenizer

# Create virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install required packages
pip install tokenizers python-dotenv openai tenacity tqdm
```

## Configuration

1. Create a `.env` file in the project root:
```
OPENAI_API_KEY=your_api_key_here
```

2. Customize the tokenizer settings in the code (optional):
```python
vocab_size=30000  # Adjust vocabulary size
special_tokens=["[PAD]", "[UNK]", "[CLS]", "[SEP]", "[MASK]"]  # Modify special tokens
```

## Usage

```python
# Run the tokenizer training script
python security_tokenizer.py
```

### Using the Trained Tokenizer

```python
from tokenizers import ByteLevelBPETokenizer

# Load the trained tokenizer
tokenizer = ByteLevelBPETokenizer.from_file("security_tokenizer/vocab.json", "security_tokenizer/merges.txt")

# Tokenize a security log
log = "May 15 10:23:45 server sshd[12345]: Failed password for invalid user admin from 192.168.1.100 port 43215 ssh2"
encoded = tokenizer.encode(log)

# View the tokens
print(encoded.tokens)
```

## Integration Examples

### 1. Log Anomaly Detection
```python
def process_logs_for_anomalies(logs, tokenizer):
    encoded_logs = [tokenizer.encode(log) for log in logs]
    # Process encoded logs for anomaly detection
    # Add your anomaly detection logic here
```

### 2. Security Pattern Matching
```python
def identify_security_patterns(log_stream, tokenizer):
    for log in log_stream:
        tokens = tokenizer.encode(log).tokens
        # Implement pattern matching logic
        # Add your security pattern detection here
```

## Best Practices

1. **Training Data Management**
   - Regularly update training data with new log formats
   - Include logs from all your cloud services
   - Maintain a balance of different log types

2. **Tokenizer Optimization**
   - Adjust vocabulary size based on your use case
   - Fine-tune special tokens for your specific needs
   - Regularly retrain with new security log patterns

3. **Integration Guidelines**
   - Use batch processing for large log volumes
   - Implement proper error handling
   - Consider rate limiting for API calls

## Limitations

- Training data quality depends on GPT-4 generated logs
- Requires OpenAI API access for initial data generation
- May need customization for specific cloud provider formats

## Future Enhancements

- [] Support for more cloud provider log formats
- [] Integration with popular SIEM systems
- [] Real-time log processing capabilities
- [] Custom training data integration
- [] Performance optimizations for large-scale deployment


