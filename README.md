# Companion-API
This is the repository for a REST API created by me using FastAPI to manipulate MTG Companion / Eventlink applications and its GraphQL API as a study case. It provides full control over tournaments in MTG Companion and can be used to integrate with your own tournament or store website. 

There's a working swagger with complete information about this API, you can check it out here: https://companion.matheusramos22.repl.co/docs

Aside from that, here is a full get started guide to newcomers:

-- How to get started guide

--- Companion Account:
    1 - First, you need a Wizards/Companion Account, head to https://myaccounts.wizards.com/register and create your account.


--- API Authentication:
    2 - Our api uses authentication, we provide a test account so anyone can access it, you must post to this address: https://companion.matheusramos22.repl.co/login and provide this data as a body request: 'username': 'test@github.com', 'password': '123456'.It will respond with your granted access token.


--- Companion Token:
    3 - Post to https://companion.matheusramos22.repl.co/companion_token, including as your header: 'authorization' with value'Bearer YOUR_GRANTED_ACCESS_TOKEN'. For the rest of this get started guide you must insert this header to ensure you're authenticated. Include your wizards account as params in this manner: 'user': YOUR_WIZARDS_ACCOUNT_EMAIL, 'password': YOUR_WIZARDS_ACCOUNT_PASSWORD. It will respond with your companion token as 'token'.


--- Create an Event:
    4 - Post to https://companion.matheusramos22.repl.co/create_event using authentication header, and as params: 'token': YOUR_COMPANION_TOKEN, 'title_event': CHOOSE_YOUT_EVENT_TITLE, 'format_type': CHOOSE_YOUR_EVENT_FORMAT. It will respond with your created companion tournament event id (COMPANION_EVENT_ID) and event code.


--- Add Player:
    5 - Post to https://companion.matheusramos22.repl.co/add_player using authentication header, and as params: 'token': YOUR_COMPANION_TOKEN, 'first_name': CHOOSE_PLAYERS_NAME, 'event_id': COMPANION_EVENT_ID.

You can use step 5 to include as many players as you want, you must include at least 2 players to start an event.


--- Start Event:
    6 - Post to https://companion.matheusramos22.repl.co/start_event using authentication header, and as params: 'token': YOUR_COMPANION_TOKEN, 'event_id': COMPANION_EVENT_ID. It will respond with a tournament status indicating that the tournament has been succesful created.
    
    
--- Next Round:
    7 - Post to https://companion.matheusramos22.repl.co/next_round using authentication header, and as params: 'token': YOUR_COMPANION_TOKEN, 'event_id': COMPANION_EVENT_ID. It will respond with a tournament status indicating round matches.
    
    
 --- Round Results:
     8 - Post to https://companion.matheusramos22.repl.co/round_results using authentication header, as params: 'token': YOUR_COMPANION_TOKEN, 'event_id', and as in request body this layout (data to produce this layout can be obtained in the next round response (item 7): 
        pairing = {
                    'table': TABLE,
                    'match_id': MATCH_ID,
                    'player1Id': PLAYER1_ID,
                    'player2Id': PLAYER2_ID,
                    'player1Name': PLAYER1_NAME,
                    'player2Name': PLAYER2_NAME,
                    'player1Score': PLAYER1_SCORE,
                    'player2Score': PLAYER2_SCORE
                    }
              
              
--- End Event:
    9 - Post to https://companion.matheusramos22.repl.co/end_event using authentication header, and as params: 'token': YOUR_COMPANION_TOKEN, 'event_id': COMPANION_EVENT_ID. It will respond with final tournament results indicating it has been sucessful ended.
    
    
-- Extra Features:

   1 - You can get to https://companion.matheusramos22.repl.co/active_events using authentication header, and as params: 'token': YOUR_COMPANION_TOKEN. It will retrieve all currently going events in your companion account, including event_id's.
   
   2 - You can get to https://companion.matheusramos22.repl.co/event_data using authentication header, and as params: 'token': YOUR_COMPANION_TOKEN, 'event_id': COMPANION_EVENT_ID. It will retrieve all currently information about this specific tournament, including round results, date, players scores, format, name, and much more information.
   
I hope this covers all common use cases and I advise to use the aforementioned swagger so you can properly use this api. 

In case you have any questions, please get in touch with me. It'll be a pleasure to help you out.
