Seun Onile-ere (29/05/17) Task 3: Fireside_Fixture_Manager
This program is being created so that leaderboard fixtures may be be determined for each player attempting to enter the Fireside Annual Card Gaming Leauge, sourcing these inputted fixtures played/results from the relevant files holding the fixture data.


    #Displays the welcome message that associates the player with the context of the program 
    print ('---------->>>Welcome to the Fireside Fixture Manager<<<---------- \n')

    #Creates a while loop pertaining to a duration in time whilst the variable 'Player_Selection' is equal to the value 'True'
    Player_Selection = True
    while Player_Selection:
    #While the previous statement is still in effect, the string containing the 'Option Menu' below will be printed, which entails a display of the program's possesion of 4 selectable options 
        print (""" The 'Option Menu' for this particular program consists of 4 possible options:
        1.Option A: Search for a fixture (Press a to do so)
        2.Option B: Outstanding fixtures (Press b to do so)
        3.Option C: Display Leader Board (Press c to do so)
        4.Exit/Quit (Press q to do so)
        """)
    #Creates a presence check for the variable 'Player_Selection', meaning whilst the user input in response to the prompt is equal to a blank space (''), the user will be prompted to re-enter  
        Player_Selection = input("Please select an appropraite option from those given above.  ")
        while Player_Selection == '':
         Player_Selection = input('Unfortunately this input does not contain any notable data; please re-enter the option chosen:  \n')
    #States that if the user input in response to the prompt is equal to a, b, c or q, a reciprocal message will be displayed and the program will proceed, else the program will loop to the start  
        if Player_Selection!= 'a' or 'b' or 'c' or 'q':
            print('Thank you for entering your option, as to confirm its validity. ')

    #States that if the variable 'Player_Selection' equates to the value of 'a', then the string 'Option A has been selected: Search for a fixture.', will be printed        
        if Player_Selection == "a": 
          print("\n Option A has been selected: Search for a fixture.")
    #The code which harbours the risk of an exception, is embedded in a 'try' block, whilst the statement 'except' pardons the 'ValueError' caused by a possible non-integer value being entered    
          try:
              Fixture_Number = int(input('Please enter your given fixture number.  \n'))
          except ValueError:
    #In this instance due to the error of a non-integer value (int) being inputted during the execution of a program, a warning message is printed that the program will return to the options menu        
              print ('Error: This fixture number is not recognised by the program, and thus is invalid - the program will now return to the options menu.  \n')
    #Following the previous message having been printed, the statement 'continue' will then be used to return the control to the beginning of the program          
              continue
    #States that if the variable 'Fixture_Number' is either less than or equal to '0'/greater than or equal to '191', an error message will be printed and the program will loop back to the start      
          if Fixture_Number <=0 or Fixture_Number >=191: 
                print ('Error: This fixture number is not recognised by the program, and thus is invalid - the program will now return to the options menu.  \n')
    #Otherwise, if 'Fixture_Number' is within an ideal range, the program will then use the 'with' statement and 'open()' function to open the 'firesideFixtures.txt' file as the logical file 'fp'           
          else:        
              with open("firesideFixtures.txt") as fp:
    #States that the variable 'Player_Fixture' equates to the value of the variable 'Fixture Number - 1', whilst variable 'lines' equates to logical file 'fp' being read with function 'readlines'              
                    Player_Fixture = Fixture_Number - 1
                    lines = fp.readlines()
    #After, the variable 'Player_Fixture' is used to identify which line that the variable 'lines' selects and reads as the user's selected fixture - the statement 'break' terminating the loop              
                    print (lines[Player_Fixture]) 
                    break
                
    #States that if the variable 'Player_Selection' equates to the value of 'b', then the string 'Option B has been selected: Outstanding fixtures.', will be printed
        elif Player_Selection == "b":
          print("\n Option B has been selected: Outstanding fixtures.")
    #Prints two strings, the first being 'These are the fixtures that have not been played yet :', and the second being the format in which the outstanding fixtures will be printed       
          print ('These are the fixtures that have not been played yet :  \n')
          print ('''The format of the fixtures will be:
          Fixture Number, Fixture Date, Fixture Time, Player 1 Nickname, Player 2 Nickname.''')
    #States that the program will use the 'open()' function to open the 'firesideFixtures.txt' file within the logical file 'ft', with aid of the 'read' function (r)
          ft = open("firesideFixtures.txt","r")
    #Uses a for loop to state that if the string value 'Y' is not within the line of code being read, then that line should be printed; otherwise that line of code will not be printed      
          for line in ft:
              if 'Y' not in line:
                  print (line)
    #States that the variable 'Total_Outstanding is equal to the value '[190-121]', which represents the point after line '121' when string value 'Y' doesn't appear on the file's lines of code              
          TotalOutstanding = ([190-121])
    #Prints the string 'According to our data, the total number of fixtures outstanding are' ,TotalOutstanding,', which displays outstanding fixtures - the statement 'break' terminating the loop      
          print ('According to our data, the total number of fixtures outstanding are' ,TotalOutstanding,'\n')
          break         

    #States that if the variable 'Player_Selection' equates to the value of 'c', then the string 'Option C has been selected: Display Leader Board.', will be printed
        elif Player_Selection == "c":
          print("\n Option C has been selected: Display Leader Board.")
    #Prints the string 'These are the current leaderboards: Player Nickname, Matches Played, Matches Won, Points', which entails the format for how the leaderboard results are going to be shown    
          print (''' These are the current leaderboards:
                 Player Nickname, Matches Played, Matches Won, Matches Lost,
                 Points''')
    #The program will then use the 'with' statement and 'open()' function to open the 'firesideResults.txt' file as the logical file 'infile'
          with open('firesideResults.txt') as infile:
    #Uses a for loop to state that if the string value '0' is not within the line of code being read, variable 'current' will be made from using the 'split' function on 'line' to unconcatenate it        
              for line in infile:
                  if '0' not in line:
    #First, variable results will then equate to the third element within the variable 'current', then function 'map' will call (int) on each item and the return values will collect as a new list                   
                      current = (line.split(','))
                      results = current[2]
                      results = list(map(int, results))
    #Next, variable 'answer' will be the sequence within variable 'results' * 3, with variable 'points' being the sum of those values, before printing the values of variables 'line' and 'points'                  
                      answer = (results*3)
                      points =(sum(answer))
                      print (line,points)
    #Finally, the aformentioned variable 'Player_Selection' will equate to the value 'False', thus terminating the loop sustained from the start of the program, of when 'Player_Selection = True'                  
                      Player_Selection = False

    #States that if the variable 'Player_Selection' equates to the value of 'q', then the string 'Exit/Quit has been selected.', will be printed
        elif Player_Selection == "q":
          print("\n Exit/Quit has been selected.")
    #Prints the string 'Thank you for your time, any Fireside Fixture Manager data has been saved and secured. The program will now terminate.', using the statement 'break' to terminate the loop      
          print('''\n Thank you for your time, any Fireside Fixture Manager data has been saved and secured.
                The program will now terminate.''')
          break


