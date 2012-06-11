![image](https://github.com/Experiments/popper-design/blob/master/popper_overview.png?raw=true)

1. Researcher downloads the Popper SDK from Github using their desktop Github client. 

2. Researcher opens the Popper SDK in Unity and creates an experiment consisting of the Client and Master Client. The Client is the visual front end of the experiment. It is ultimately executed on a player's computer or phone. The Master Client is the underlying logic of the experiment and ultimately runs in the Experiment Server.

3. Researcher uploads the experiment, which consists of the Master Client, Client, and Source Code, to his local GitHub repository. 

4. GitHub Client syncs the contents of the local repository with the remote online GitHub repository. 

5. Researcher logs into the online Researcher Dashboard and selects an experiment to launch a trial. 

6. The Popper Web Service downloads the Master Client that corresponds to the selected experiment.

7. The Popper Web Service uploads this Master Client to the Experiment Server.

8. The Popper Web Service remotely starts the Master Client on the Experiment Server and connects it to the Photon Server, creating a trial. 

9. The Popper Web Service announces the trial to eligible players in the Popper Subject Pool.

10. Interested players log into the Player Site. 

11. The Player Site downloads the Client from the experiments repository on GitHub.

12. The Player Site opens the Client on each player's browser or phone. The player sees the game.

13. Each player's Client connects to the current trial running on the Photon Server.

14. The Popper Web Service establishes a connection with Photon Server via Photon Client. 
The trial begins.

15. The Researcher Site monitors the ongoing trial via Photon Client.

16. All events in the trial are recorded in the Popper database.

17. Researcher monitors the ongoing trial in his browser. Once the trial ends, Researcher reviews and approves subject payments.

18. The Popper Web Service posts payments to players' accounts. 