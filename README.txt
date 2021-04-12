An implementation of Byzantine Chain Replication based on-

van Renesse R., Ho C., Schiper N. (2012) Byzantine Chain Replication. In: Baldoni R., Flocchini P., Binoy R. (eds) Principles of Distributed Systems. OPODIS 2012. Lecture Notes in Computer Science, vol 7702. Springer, Berlin, Heidelberg

The described system requires 2t+1 replicas to tolerate t Byzantine failures.

Motivation

This was done as course project for the course CSE 535 Asyschronous Systems at Stony Brook University taught by Professor Scott Stoller.

PLATFORM
OS: Windows 10
DistAlgo version: 1.0.9
Python implementation: CPython
Python version: 3.5

INSTRUCTION
1. Unzip the release zip in your Windows 10 PC. Go to the root of the unzipped folder.
2. Put your config file in config folder.
3. Open two command line terminals
4. In the first terminal run the following command with <config_file_name.txt> as the argument
    python -m da --logfile -n MainNode --logfilename logs\log_verify_result_single_client_2_mainnode.txt -F info --message-buffer-size 100000  src\bcr.da <config_file_name.txt>
5. In the second terminal run the following command with <config_file_name.txt> as the argument
    python -m da --logfile -n ClientNode --logfilename logs\log_verify_result_single_client_2_clientnode.txt -F info --message-buffer-size 100000  src\bcr.da <config_file_name.txt>

For example to run test case 1:
1. open 2 command line terminals
2. on terminal 1 run the following command-
    python -m da --logfile -n MainNode --logfilename logs\log_verify_result_single_client_2_mainnode.txt -F info --message-buffer-size 100000  src\bcr.da config_result_verify_testcase_2.txt
2. on terminal 2 run the following command-
    python -m da --logfile -n ClientNode --logfilename logs\log_verify_result_single_client_2_clientnode.txt -F info --message-buffer-size 100000  src\bcr.da config_result_verify_testcase_2.txt

WORKLOAD GENERATION
Algorithm:
pseudorandom(seed, n):
    initialize python's random number generator with the specified seed.
    for i in range(n):
        generate a random number from 1 to 4 and map it to (get put slice append)
        generated key and value using random to generate 4 random lowercase character

CONTRIBUTIONS
Keshav Gupta:
    PHASE 2:
    olympus- create initial configuration: create keys, create, setup, and start processes
    generate pseudorandom workload with good diversity using specified seed
    all key generations and signature checks and validations
    timeout and send request to all replicas if timely response not received
    methods of dictionary object except slice and append
    handle retransmitted request as described in paper
    statement and signed result statement, send updated shuttle
    check validity of order proof (incl. signatures), add signed order
    check that dictionary contains expected content at end of test cases
    PHASE 3:
    reconfiguration flow on replica and olympus
    sign, validation of client requests
    ask olympus if config changed periodically, proof of misbehaviour by client

Pratik Sushil Zambani:
    PHASE 2:
    support configuration files specified in project.txt
    generate request sequence specified in config file
    implementation append and slice in dictionary
    head: handle new request: assign slot, result stmt, send shuttle
    tail: send result to client; send result shuttle to predecessor
    handle result shuttle save, and forward it
    fault-injection: required triggers
    fault-injection: required failures
    PHASE 3:
    checkpoint flow
    fault-injection: required triggers
    fault-injection: required failures


MAIN FILES
src/bcr.da
src/client.da
src/object.py
src/olympus.da
src/replica.da
