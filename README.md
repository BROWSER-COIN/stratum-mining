stratum-mining
==============

Demo implementation of bitcoin mining pool using Stratum mining protocol.

For Stratum mining protocol specification, please visit http://mining.bitcoin.cz/stratum-mining.

run
-------

#### 1. install requirments
```bash
pip install -r requirments.txt
```

#### 2. install stratum
_pip install stratum_ failed. Install it manually.
```bash
git clone https://github.com/slush0/stratum.git
cp -r stratum/stratum stratum-mining/
```

#### 3. modify websocket_transport.py
```bash
cd stratum-mining
vi stratum/websocket_transport.py
replace "from autobahn.twisted.websocket" with "from autobahn.websocket"
```

#### 4. modify coinbaser.py
The new rpc `validateaddress` response doesn't contain `ismine`
```bash
vi lib/coinbaser.py
replace "if result['isvalid'] and result['ismine']:" with "if result['isvalid']:"
```

#### 5. modify config
```bash
vi conf/config_sample.py
LOGDIR = 'log/'
LOGFILE = 'stratum.log'
HOSTNAME = '192.168.30.106'
BITCOIN_TRUSTED_HOST = 'localhost'
BITCOIN_TRUSTED_PORT = 17116
BITCOIN_TRUSTED_USER = 'bitcoinrpc'
BITCOIN_TRUSTED_PASSWORD = '123456'
CENTRAL_WALLET = 'mvoZ4EfQG4DFCv9wAqszbAVtNykfSniZ3A'
```

#### 6. start stratum
```bash
mkdir log
mv conf/config_sample.py conf/config.py
nohup twistd -ny launcher_demo.tac -l - >/dev/null 2>&1 &
```