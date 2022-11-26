# loan_calculator

import math
import argparse
# parser = argparse.ArgumentParser()
# parser.add_argument("--type", choices= ["annuity", "diff"] , help="Incorrect parameters")
# parser.add_argument("-i2","--ingredient_2", choices= ["pasta", "rice", "potato",
#                     "onion", "garlic", "carrot", "soy_sauce", "tomato_sauce"],
#                     help="You need to choose only one ingredient from the list.")
# parser.add_argument("-i3","--ingredient_3", choices= ["pasta", "rice", "potato",
#                     "onion", "garlic", "carrot", "soy_sauce", "tomato_sauce"],
#                     help="You need to choose only one ingredient from the list.")
# parser.add_argument("-i4","--ingredient_4", choices= ["pasta", "rice", "potato",
#                     "onion", "garlic", "carrot", "soy_sauce", "tomato_sauce"],
#                     help="You need to choose only one ingredient from the list.")
def diff(i_per,P1,periods1):
    # i_per = 10
    i = float(i_per)/(12 * 100)
    P = float(P1)
    periods = int(periods1)
    act_payment = 0
    for a in range(1,periods+1):
        print(f'Month {a}: payment is {math.ceil((P/periods)+(i*(P - ((P* (a-1)/periods)))))}')
        act_payment = act_payment + math.ceil((P/periods)+(i*(P - ((P* (a-1)/periods)))))
    print(f'\nOverpayment = {int(act_payment - P)}')

def principal(A1,periods1,i_per):
    A = float(A1)
    periods = int(periods1)
    # i_per = 5.6
    i = float(i_per) / (12 * 100)
    print(f'Your loan principal = {math.ceil(A / (((i * math.pow((1 + i),periods))/ (math.pow((1 + i),periods) - 1))))}!')
    print(f'Overpayment = {int(A * periods - math.ceil(A / (((i * math.pow((1 + i),periods))/ (math.pow((1 + i),periods) - 1)))))}')

def ann(i_per,P1,periods1):
    P = float(P1)
    periods = int(periods1)
    # i_per = 10
    i = i = float(i_per)/(12 * 100)
    print(f'Your annuity payment = {math.ceil(P * (((i * math.pow((1 + i),periods))/ (math.pow((1 + i),periods) - 1))))}!')
    print(f'Overpayment = {int((periods * math.ceil(P * (((i * math.pow((1 + i),periods))/ (math.pow((1 + i),periods) - 1))))) - P)}')


def perio(P1,A1,i_per):
    P = float(P1)
    A = float(A1)
    # i_per = 7.8
    i = float(i_per) / (12 * 100)
    periods = math.ceil(math.log((A/(A - i * P)),1 + i))
    y = periods // 12
    m = math.ceil((periods % 12) * 12)
    m = periods % 12
    if y == 0:
        print(f'It will take {m} months to repay this loan!')
    elif m == 0:
        print(f'It will take {y} years to repay this loan!')
    else:
        print(f'It will take {y} years and {m} months to repay this loan!')
    print(f'Overpayment = {int(A * periods - P)}')

parser = argparse.ArgumentParser()
parser.add_argument("--type")
parser.add_argument("--principal")
parser.add_argument("--periods")
parser.add_argument("--interest")
parser.add_argument("--payment")

args = parser.parse_args()
if args.type not in ['diff','annuity']:
    print('Incorrect parameters')
elif args.type == 'diff':
    if args.payment != None:
        print('Incorrect parameters')
    else:
        diff(args.interest,args.principal,args.periods)
elif args.type == 'annuity':

    if args.principal == None and args.payment != None and args.periods != None and args.interest != None:
        principal(args.payment,args.periods,args.interest)
    elif args.payment == None and args.principal != None and args.periods != None and args.interest != None:
        ann(args.interest,args.principal,args.periods,)
    elif args.periods == None and args.payment != None and args.principal != None and args.interest != None:
        perio(args.principal,args.payment,args.interest)

    else:
        print('Incorrect parameters')
