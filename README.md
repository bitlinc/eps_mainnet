# Electrum Personal Server configuration file
  
# Lines starting with # are called comments which are ignored.
# For a line to have effect it must not start with #

# The most important options are towards the top of the file

[master-public-keys]
# Add electrum wallet master public keys to this section
# In electrum then go Wallet -> Information to get the mpk

mainnet_masterpublickey = replacempkmainnet

# Multiple master public keys maybe added by simply adding another line
#my_second_wallet = xpubanotherkey

# Multisig wallets use format `required-signatures [list of master pub keys]`
# this example is a 2-of-3 multisig wallet
#multisig_wallet = 2 xpub661MyMwAqRbcFseXCwRdRVkhVuzEiskg4QUp5XpUdNf2uGXvQmnD4zcofZ1MN6Fo8PjqQ5cemJQ39f7RTwD$


[bitcoin-rpc]
host = 127.0.0.1
port = 8332
#add the bitcoin datadir to search for the .cookie file created by the
# node, which avoids the need to configure rpc_user/pass
#leave this option empty to have it look in the default location
datadir =
#if you dont want to use the .cookie method with datadir, uncomment to config u/p here
rpc_user = var2
rpc_password = bin1

#to be used with the multi-wallet feature
# see https://github.com/bitcoin/bitcoin/blob/master/doc/release-notes/release-notes-0.15.0.md#multi-wallet-$
# empty means default file, for when using a single wallet file
wallet_filename =

# how often in seconds to poll for new transactions when electrum not connected
poll_interval_listening = 30
# how often in seconds to poll for new transactions when electrum is connected
poll_interval_connected = 5

# Parameters for dealing with deterministic wallets
# how many addresses to import first time, should be big because if you import too little you may have to re$
initial_import_count = 2000
# number of unused addresses kept at the head of the wallet
gap_limit = 25

[electrum-server]
# 0.0.0.0 to accept connections from any IP
#127.0.0.1 to accept from only localhost
host = 127.0.0.1
port = 50002

# space-separated whitelist of IP addresses
# accepts CIDR notation eg 192.168.0.0/16 or 2a01:4f8:1f1::/120
# star (*) means all are accepted
# generally requires host binding (above) to be 0.0.0.0
ip_whitelist = *

#SSL certificate
#uses the default one, which is fine because by default nobody should be
# allowed to connect to your server or scan your packets
#to generate another certificate see https://github.com/spesmilo/electrum-server/blob/ce1b11d7f5f7a70a3b6cc7$
certfile = certs/cert.crt
keyfile = certs/cert.key

# Option for disabling the fee histogram calculation
# It improves server responsiveness but stops mempool-based Electrum features
# This is useful on low powered devices at times when the node mempool is large
disable_mempool_fee_histogram = true

# Parameter for broadcasting unconfirmed transactions
# Options are:
# * own-node         (broadcast using the connected full node)
# * system <cmd> %s  (save transaction to file, and invoke system command
#                     with file path as parameter %s)
#                     with file path as parameter %s)
broadcast_method = own-node

[watch-only-addresses]
#Add individual addresses to this section, for example paper wallets
#Dont use this section for adding entire wallets, instead use the
# above section `master-public-keys`

#addr = 1DuqpoeTB9zLvVCXQG53VbMxvMkijk494n

# A space separated list is also accepted
#my_test_addresses = 3Hh7QujVLqz11tiQsnUE5CSL16WEHBmiyR 1PXRLo1FQoZyF1Jhnz4qbG5x8Bo3pFpybz bc1qar0srrr7xfkvy$

# multiple addresses may also be added in separate lines (like master public keys above)
#addr2 = 3anotheraddress

[logging]
# Section for configuring the logging output

# The log level. Logging messages less severe than this will not be displayed
#options are 'DEBUG', 'INFO', 'WARNING', 'ERROR', 'CRITICAL'
#Information printed to the log file is always at level DEBUG
log_level_stdout = INFO

# Location of log file, leave empty to use the default location in temp dir
log_file_location = /home/pi/eps_mainnet/electrum-personal-server/log.txt

# Whether to append to log file or delete and overwrite on startup
append_log = false

# Format to use for logging messages
#see docs https://docs.python.org/3/library/logging.html#logging.Formatter
log_format = %(levelname)s:%(asctime)s: %(message)s
