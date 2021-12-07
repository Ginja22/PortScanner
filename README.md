#ProjectB
import sys
from pyfiglet import Figlet
import datetime
import socket


# Here are my libraries
# Figlet help assisted by: (Stackoverflow.com, member "penta", on 10/2016)
f = Figlet(font='digital')
fs = Figlet(font='epic')
print(f.renderText("*****************************"))
print(fs.renderText("Elaine's Port\nScanner"))
print(f.renderText("*****************************"))

#Created a text file to show all the results.
scn_fl = open("Elainesportscanner.txt", "w")
scn_fl.write("Swooosh, here it is!\n\n")

#Ask the user for a target to scan & obtain the IP address of the target.
target = input("Pick a host, any host:")
host_ip = socket.gethostbyname(target)
print("{} : {}".format(target, host_ip))

# Print a nice banner with information on which host we are about to scan
print("Please wait, scanning remote host", host_ip)
print("-" * 50)

# This is to check what time the scan started
t1 = datetime.datetime.now()
print(t1)
scn_fl.write("Starting time is" + str(t1) + "\n\n")

port = 1

#Setup for scan loop
port = 1

try:

    for port in range(1, 1025):
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(0.1)
        result = sock.connect_ex((host_ip, port))
        if result == 0:
            print("Port {}: Open".format(port))

            sock.close()


except KeyboardInterrupt:
        print("You pressed Ctrl+C,Exiting...")
        sys.exit()
except socket.gaierror:
        print('Hostname could not be resolved. Exiting...')
        sys.exit()
except socket.error:
        print("Couldn't connect to server, Exiting")
        sys.exit()
finally:
        # This block is always executed
        # Regardless of exception error
        print('This is always executed')

# Checking the start time to end time again
t2 = datetime.datetime.now()
print(t2)
scn_fl.write("Ending time is" + str(t2) + "\n\n")

# This calculates the total time it took for the port scan.
t3 = t2 - t1

# Printing the information to screen
scn_fl.write("The start time was {t1}\n The ending time was {t2}\n The total scan time was {t3}\n Thank you very much!")
print("The start time was {}\n The ending time was {}\n The total scan time was {}\n Thank you!".format(t1, t2,
                                                                                                                t3))
print(t3)
print("Thank you very much for using Elaine's Port Scanner!")

scn_fl.close()
