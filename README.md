#!/bin/bash
 
map=("0" "1" "2" "3" "4" "5" "6" "7" "8")
 
clear

echo "Это игра в крестики-нолики. Что бы выбрать клетку в которую будет ставиться кресстик введите номер свободной клетки."
 
function print_map {
    echo "Поле игры:"
    echo "${map[0]} | ${map[1]} | ${map[2]}"
    echo "${map[3]} | ${map[4]} | ${map[5]}"
    echo "${map[6]} | ${map[7]} | ${map[8]}"
}
 
function check {
        #горизантали
        if [[ (${map[0]} == ${map[1]}) && (${map[1]} == ${map[2]}) ]]; then
                echo "${map[0]} Победа"; exit;  fi
        if [[ (${map[3]} == ${map[4]}) && (${map[4]} == ${map[8]}) ]]; then
                echo "${map[3]} Победа"; exit;  fi
        if [[ (${map[6]} == ${map[7]}) && (${map[7]} == ${map[9]}) ]]; then
                echo "${map[6]} Победа"; exit;  fi
    #вертикали
        if [[ (${map[0]} == ${map[3]}) && (${map[3]} == ${map[6]}) ]]; then
                echo "${map[0]} Победа"; exit;  fi
        if [[ (${map[1]} == ${map[4]}) && (${map[4]} == ${map[7]}) ]]; then
                echo "${map[1]} Победа"; exit;  fi
        if [[ (${map[2]} == ${map[5]}) && (${map[5]} == ${map[8]}) ]]; then
                echo "${map[2]} Победа"; exit;  fi
    #диагонали
        if [[ (${map[0]} == ${map[4]}) && (${map[4]} == ${map[8]}) ]]; then
                echo "${map[0]} Победа"; exit;  fi
        if [[ (${map[2]} == ${map[4]}) && (${map[4]} == ${map[6]}) ]]; then
                echo "${map[2]} Победа"; exit; fi               
}
 
print_map

function player_turn {
    echo "Игрок:"
    read -n 1
rep=${REPLY:0:1}
}

function computer_turn {
    rep=$(( RANDOM % 9 ))
}
# Компьютер делает первый ход

for i in {1..8}
do
    if [[ $i%2 -eq 0 ]]
    then
        player_turn
        map[$rep]="O"
    else
        computer_turn
        while [[ ${map[$rep]} != $rep ]] 
        do
            computer_turn
        done
        map[$rep]="X"
    fi

    print_map

    check
    
done
    echo "Ничья"
exit