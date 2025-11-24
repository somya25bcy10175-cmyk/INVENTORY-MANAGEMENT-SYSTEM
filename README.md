% -------------------------------
% Inventory Management System
% -------------------------------

:- dynamic item/3.
% item(ID, Name, Quantity).

% Add a new item
add_item(ID, Name, Quantity) :-
    \+ item(ID, _, _),
    assert(item(ID, Name, Quantity)),
    write('Item added successfully!'), nl.

add_item(ID, _, _) :-
    item(ID, _, _),
    write('Error: Item with same ID already exists!'), nl.

% Remove an item
remove_item(ID) :-
    item(ID, Name, _),
    retract(item(ID, Name, _)),
    write('Item removed successfully!'), nl.

remove_item(_) :-
    write('Error: Item not found!'), nl.

% Update quantity
update_quantity(ID, NewQ) :-
    item(ID, Name, _),
    retract(item(ID, Name, _)),
    assert(item(ID, Name, NewQ)),
    write('Quantity updated!'), nl.

update_quantity(_, _) :-
    write('Error: Cannot update quantity, item not found!'), nl.

% Search item
search_item(ID) :-
    item(ID, Name, Quantity),
    write('Item Found: '), nl,
    write('ID: '), write(ID), nl,
    write('Name: '), write(Name), nl,
    write('Quantity: '), write(Quantity), nl.

search_item(_) :-
    write('Item not found!'), nl.

% Display Inventory
display_inventory :-
    write('--- Inventory Items ---'), nl,
    item(ID, Name, Quantity),
    write(ID), write(' | '), write(Name), write(' | Qty: '), write(Quantity), nl,
    fail.

display_inventory.

