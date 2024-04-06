import random

def invite_friends():
    num_friends = int(input("Enter the number of friends joining (including you):\n"))

    if num_friends <= 0:
        print("No one is joining for the party")
        return

    friends_dict = {}

    print("Enter the name of every friend (including you), each on a new line:")
    for _ in range(num_friends):
        friend_name = input()
        friends_dict[friend_name] = 0

    total_bill = float(input("Enter the total bill value:\n"))

    if total_bill <= 0:
        print("Invalid total bill value")
        return

    split_amount = round(total_bill / num_friends, 2)

    for friend in friends_dict:
        friends_dict[friend] = split_amount

    print(friends_dict)

    # Ask user if they want to use the "Who is lucky?" feature
    use_lucky_feature = input("Do you want to use the 'Who is lucky?' feature? Write Yes/No:\n")

    if use_lucky_feature.lower() == 'yes':
        lucky_one = random.choice(list(friends_dict.keys()))
        print(f"{lucky_one} is the lucky one!")
        friends_dict[lucky_one] = 0  # Set lucky one's share to 0

    else:
        print("No one is going to be lucky")

    # Recalculate split values for non-lucky friends
    num_non_lucky_friends = num_friends - 1 if use_lucky_feature.lower() == 'yes' else num_friends
    split_amount_non_lucky = round(total_bill / num_non_lucky_friends, 2)

    for friend in friends_dict:
        if friends_dict[friend] != 0:  # Skip updating the lucky one's share
            friends_dict[friend] = split_amount_non_lucky

    print(friends_dict)

invite_friends()
