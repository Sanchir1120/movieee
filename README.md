# movieee
# You can use the range function to create a list of numbers.
seats_range = list(range(1,16))
# Following are the slots for the movies:
available_slots = ['morning', 'afternoon', 'evening']
# You can put movies in a list.
movies_list = ["The Batman", "The Lost City", "Priusnii Boss", "The Dark Knight", "Sonic 2", "The Dark Knight Rises"]
# The dictionary is a collection of key-value pairs. Use to store data for booking.
data = {}

while True:

    # show welcome message
    print ('='*50)
    print("Welcome to Sanchirs movie booking system")
    print ('='*50)

    # ask for user's name
    name = input("Please enter your name: ")
    # ask for user's phone number
    phone = input("Please enter your phone number: ")
    # validating the phone
    while not phone.isdigit():
        phone = input("* Please enter your phone number: ").strip()

    # CHOOSE MOVIE
    print ("Please choose a movie: ")
    for index, movie_name in enumerate(movies_list, start=1):
        print ('({}) {}'.format(index, movie_name))
    movie = input(': ').lower().strip()
    # validating the input
    while movie.isdigit() and int(movie) not in range(1, len(movies_list)+1):
        movie = input("* Invalid movie choice, please choose a movie: ").lower().strip()
    movie = movies_list[int(movie)-1]
    print("You have chosen {}".format(movie))

    # CHOOSE SLOT
    slot = input("Please choose morning (1), afternoon (2) or evening (3): [i.e 1, 2, 3]: ").lower().strip()
    # validating the input
    while not slot.isdigit() or int(slot) not in range(1, len(available_slots)+1):
        slot = input("* Invalid choice please enter in range: [i.e 1, 2, 3]: ").lower().strip()
    slot = available_slots[int(slot)-1]
    print ("You have chosen {}".format(slot))


    already_booked = []
    # available seats
    print ("Available seats: ")
    for i, seat in enumerate(seats_range, start=1):
        # checking if the seat is already booked
        if movie in data:
            if slot in data[movie]:
                if seat in data[movie][slot]:
                    # if the seat is already booked, add it to the list
                    already_booked.append(seat)
                    print("[X]", end=" ")
                    continue
        print("[{}]".format(seat), end=" ")
        if i % 5 == 0:
            print()

    # choose seat
    seat = input(": ").lower().strip()
    # validating the input
    while not seat.isdigit() or int(seat) not in seats_range:
        seat = input("* Invalid choice, please choose a seat: ").lower().strip()
    seat = seats_range[int(seat) - 1]
    # check if the seat is already booked
    while seat in already_booked:
        seat = input("* This seat is already booked, please choose another one: ")
        seat = seats_range[int(seat) - 1]

    print ("You have chosen seat {}".format(seat))

    # confirm
    confirm = input("Are you sure you want to book seat `{}` for `{}`? [y/n]: ".format(seat, movie))
    # validating the input
    while confirm not in ['y', 'n']:
        confirm = input("* Invalid choice, enter y or n: ").lower().strip()
    if confirm == 'y':
        if already_booked:
            data[movie][slot].append(seat)
        else:
            data[movie] = {slot: [seat]}
        print("Thank you for booking `{}` for `{}` at `{}`.".format(seat, movie, slot))
        print ("Your booking: ")
        print (data)
        continue
    # start again
    start_again = input("Do you want to start again? [y/n]: ").lower().strip()
    # validating the input
    while start_again not in ['y', 'n']:
        start_again = input("* Invalid choice, enter y or n: ").lower().strip()
    if start_again == 'y':
        continue
    break
