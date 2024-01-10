#importing relevant libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

#importing book club members list from a file and printing those names
with open('Bookclubmembers.txt') as file:
    book_club_members = [line.strip() for line in file]
print(book_club_members)

#defining a decision function for a tailored welcome message depending on the attendees
def welcome_message(member_name, kieran_attending, orla_attending):
    if member_name in ['Lindsay', 'Reachbha', 'Martha']:
        return f"Welcome {member_name}. Would you like a glass of red?"
    elif member_name == 'Cathy':
        return f"Welcome {member_name}. Would you like a glass of white?"
    elif member_name == 'Orla' and not kieran_attending:
        return f"Welcome {member_name}. Would you like a glass of white?"
    elif member_name == 'Kieran' and not orla_attending:
        return f"Welcome {member_name}. Would you like a glass of red?"

#adding an exception for alternating members
kieran_attending = False
orla_attending = True

#create a loop
for member in book_club_members:
    message = welcome_message(member, kieran_attending, orla_attending)
    if message is not None:
        print(message)
        
#creating data visualisation to plot monthly consumption of red and white wine
months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sept', 'Oct', 'Nov', 'Dec']
red_wine = [4, 3, 4, 3, 4, 3, 4, 3, 4, 3, 4, 3]
white_wine = [1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2]

df = pd.DataFrame({'Month': months, 'Red Wine': red_wine, 'White Wine': white_wine})

bar_width = 0.35
bar_positions_red = np.arange(len(months))
bar_positions_white = bar_positions_red + bar_width
plt.bar(bar_positions_red, df['Red Wine'], width=bar_width, label='Red Wine', color='red')
plt.bar(bar_positions_white, df['White Wine'], width=bar_width, label='White Wine', color='yellow')

plt.xlabel('Month')
plt.ylabel('Wine Consumption (bottles)')
plt.title('Monthly Red and White Wine Consumption')
plt.xticks(bar_positions_red + bar_width / 2, months)
plt.legend()

plt.show()

#converting to arrays and summing the total annual consumption of wine
white_wine = np.array(white_wine)
print(white_wine.sum())

red_wine = np.array(red_wine)
print(red_wine.sum())

print(white_wine.sum() + red_wine.sum())