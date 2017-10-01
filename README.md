""" 
Functions for Assignment A3

This file contains the functions for the assignment.  You should replace the
stubs with your own implementations.

Angela ______ helped us with str5_cmyk().

Helen Butler (hpb33), Armine Kalbakian (ask276)
10/5/2017
"""
import cornell
import math


def complement_rgb(rgb):
    """
    Returns: the complement of color rgb.
    
    Parameter rgb: the color to complement
    Precondition: rgb is an RGB object
    """
    # THIS IS WRONG.  FIX IT
    return cornell.RGB(255-rgb.red, 255-rgb.green, 255-rgb.blue)


def round(number, places):
    """
    Returns: the number rounded to the given number of decimal places.
    
    The value returned is a float.
    
    This function is more stable than the built-in round.  The built-in round
    has weird behavior where round(100.55,1) is 100.5 while round(100.45,1) is
    also 100.5.  We want to ensure that anything ending in a 5 is rounded UP.
    
    It is possible to write this function without the second precondition on
    places. If you want to do that, we leave that as an optional challenge.
    
    Parameter number: the number to round to the given decimal place
    Precondition: number is an int or float
    
    Parameter places: the decimal place to round to
    Precondition: places is an int; 0 <= places <= 3
    """
    # To get the desired output, do the following
    #   1. Shift the number "to the left" so that the position to round to is
    #      left of the decimal place.  For example, if you are rounding 100.556
    #      to the first decimal place, the number becomes 1005.56.  If you are
    #      rounding to the second decimal place, it becomes 10055.6.  If you are
    #      rounding 100.556 to the nearest integer, it remains 100.556.
    shifted=number*(math.pow(10,places))
    #print ('shifted equals ' + str(shifted))
    #   2. Add 0.5 to this number
    shifted_with_point_five= shifted + 0.5
    #print ('shifted_with_point_five equals ' + str(shifted_with_point_five))
    #   3. Convert the number to an int, cutting it off to the right of the
    #      decimal.
    int_convert= int(shifted_with_point_five)
    #print ('int_convert equals ' + str(int_convert))
    #   4. Shift the number back "to the right" the same amount that you did to
    #      the left. Suppose that in step 1 you converted 100.556 to 1005.56.
    #      In this case, divide the number by 10 to put it back.
    result= int_convert/(math.pow(10,places))
    return result


def str5(value):
    """
    Returns: value as a string, but expand or round to be exactly 5 characters.
    
    The decimal point counts as one of the five characters.
   
    Examples:
        str5(1.3546)  is  '1.355'.
        str5(21.9954) is  '22.00'.
        str5(21.994)  is  '21.99'.
        str5(130.59)  is  '130.6'.
        str5(130.54)  is  '130.5'.
        str5(1)       is  '1.000'.
    
    Parameter value: the number to convert to a 5 character string.
    Precondition: value is a number (int or float), 0 <= value <= 360.
    """
    # Note:Obviously, you want to use the function round() that you just
    #      defined.
     
    # However, remember that the rounding takes place at a different place
    # depending on how big value is. Look at the examples in the specification.
    string_of_value=str(value)
    #print('string_of_value is ' )
    #find '.'
    # cornell.assert_equals('100.0',  a3.str5(99.995))
    # cornell.assert_equals('0.000',  a3.str5(.0004))
    location_of_decimal=string_of_value.find('.')
    if location_of_decimal==-1:
        length_of_no_decimal_string=len(string_of_value)
        if length_of_no_decimal_string==1:
            #add '.' and 000
            almost_result= string_of_value + '.' + '000'
        elif length_of_no_decimal_string==2:
            almost_result= string_of_value + '.' + '00'
        else:
             almost_result= string_of_value + '.' + '0'
    else: #('22.00',  a3.str5(21.99575))
        before_decimal=string_of_value[:location_of_decimal]
    #store the part before the '.'
    #count how long it is
        length_before_decimal=len(before_decimal)
        print ('length_before_decimal is ' + str(length_before_decimal))
    #float_length_before_decimal= int(length_before_decimal)
        if length_before_decimal ==1:
        #round it to 3
            almost_result=round(value, 3)
            print('*almost_result is ' + str(almost_result))
            str_almost_result=str(almost_result)
            x=str_almost_result.index('.')
            y=str_almost_result[x+1:]
            z=str_almost_result[:x]
            q=str_almost_result[:x+2]
            print('hopefully this says 0.0 ' + q)
            #x=str(almost_result).index('.')
            #y=str(almost_result)[x+1:]
            ####if len(z)==2:
                #add 2 more zeros
                ###almost_result=z+'.00'
                #almost result needs to be here
            ####elif str_almost_result=='0.0':
                #print('it starts with 0.0')
                #add 2 more zeros
                #####almost_result='0.000'
                #almost result needs to be here
            ####else:
                #####print('went to else')
                #####almost_result=almost_result
                #WE NEED SOMETHING HERE??
        elif length_before_decimal ==2:
            #cornell.assert_equals('10.00',  a3.str5(9.9999))
            print ('length_before_decimal == 2')
        #round it to 2
            almost_result=round(value, 2)
            print('when length_before_decimal is 2 almost_result is ' +
                  str(almost_result))
            str_almost_result=str(almost_result)
            x=str_almost_result.index('.')
            y=str_almost_result[x+1:]
            z=str_almost_result[:x]
            ######if len(z)==2:
                #####y= str(y)
                ######almost_result=z + '.' + y + '0'
            ######else:
                ######almost_result=z+'.00' #what if there's a number after
                #decimal
            #if there is a zero after decimal, add another zero
                #x=str_almost_result.index('.')
                #y=str_almost_result[x+1:]
                #######if y=='0':
                #add another zero
                    ######almost_result=str_almost_result+'0'
                    #####print('if digit after decimal is 0, just added another
                    #            0 yields ' + str_almost_result)
                #####else:
                    #####almost_result=str_almost_result
        else:
        #round it to 1
            almost_result=round(value,1)
            print('almost_result is ' + str(almost_result))
    result=str(almost_result)
    print('result is ' + result)
    if result.find('e') == 1:
        print('e in result')
        finalresult= '0.000'
        #show to armine
    elif len(result) == 2:
        print('len(result)=2')
        finalresult=result + '000'
    elif len(result) == 3:
        print('len(result)=3')
        finalresult= result + '00'
    elif len(result) == 4:
        print('len(result) = 4')
        finalresult= result+ '0'
    else:
        print('len(result) > 4')
        finalresult=result
    return finalresult


def str5_cmyk(cmyk):
    """
    Returns: String representation of cmyk in the form "(C, M, Y, K)".
    
    In the output, each of C, M, Y, and K should be exactly 5 characters long.
    Hence the output of this function is not the same as str(cmyk)
    
    Example: if str(cmyk) is 
    
          '(0.0,31.3725490196,31.3725490196,0.0)'
    
    then str5_cmyk(cmyk) is '(0.000, 31.37, 31.37, 0.000)'.
    Note the spaces after the commas. These must be there.
    
    Parameter cmtk: the color to convert to a string
    Precondition: cmyk is an CMYK object.
    """
    """When we couldn't find a way for Python to recognize cyan as an
    attribute, Angela gave us the idea to make new variables (like str_cyan)
    for the attributes after they went through the str5() function, instead of
    changing the actual attributes in the object."""
    str_cyan=str5(cmyk.cyan)
    str_magenta=str5(cmyk.magenta)
    str_yellow=str5(cmyk.yellow)
    str_black=str5(cmyk.black)
    result = '(' + str_cyan + ', ' + str_magenta + ', ' + str_yellow + ', ' + str_black + ')' #string form of color object
            #I CAN'T FIGURE OUT THE LINE SPLITTING HERE
    return result   
    
    
def str5_hsv(hsv):
    """
    Returns: String representation of hsv in the form "(H, S, V)".
    
    In the output, each of H, S, and V should be exactly 5 characters long.
    Hence the output of this function is not the same as str(hsv)
    
    Example: if str(hsv) is 
    
          '(0.0,0.313725490196,1.0)'
    
    then str5_hsv(hsv) is '(0.000, 0.314, 1.000)'. Note the spaces after the
    commas. These must be there.
    
    Parameter hsv: the color to convert to a string
    Precondition: hsv is an HSV object.
    """
    str_hue=str5(hsv.hue)
    if str_hue == '360.0':
        str_hue = '359.9'
    str_saturation=str5(hsv.saturation)
    str_value=str5(hsv.value)
    result = '(' + str_hue + ', ' + str_saturation + ', ' + str_value + ')' 
    return result


def rgb_to_cmyk(rgb):
    """
    Returns: color rgb in space CMYK, with the most black possible.
    
    Formulae from en.wikipedia.org/wiki/CMYK_color_model.
    
    Parameter rgb: the color to convert to a CMYK object
    Precondition: rgb is an RGB object
    """
    #hsv= rgb/255.0
    new_red= (rgb.red)=255.0
    print('red divided by 255.0 is ' + str((new_red))
    new_green= (rgb.green)=255.0
    print('green divided by 255.0 is ' + str((new_green))
    new_blue= (rgb.blue)/255.0
    print('blue divided by 255.0 is ' + str((new_blue))
    C1= 1 - new_red
    print ('C1 is ' + str(C1))
    M1= 1 - new_green
    print ('M1 is ' + str(M1))
    Y1= 1 - new_blue
    print ('Y1 is ' + str(Y1))
    if C1 == 1 and M1 == 1 and Y1 ==1:
        print ('C1, M1, and Y1 are all 1')
        cmyk_object = cornell.CMYK(0.000,0.000,0.000,100.0)
        print ('cmyk_object is (0.000,0.000,0.000,100.0)')
    else:
        print ('C1, M1, and Y1 are not all 1')
        K = min(C1, M1, Y1)
        print ('K equals ' + str(K))
        C = (C1 - K)/(1 - K)
        print ('C equals ' + str(C))
        M = (M1 - K)/(1 - K)
        print ('M equals ' + str(M))
        Y = (Y1- K)/(1 - K)
        print ('Y equals ' + str(Y))
        cmyk_object = cornell.CMYK(C,M,Y,K)
        print ('cmyk object has been made')
        C2= (cmyk_object.C)*100.0
        print ('C*100.0 equals ' + str(C2))
        M2= (cmyk_object.M)*100.0
        print ('M*100.0 equals ' + str(M2))
        Y2= (cmyk_object.Y)*100.0
        print ('Y*100.0 equals ' + str(Y2))
        K2= (cmyk_object.K)*100.0
        print ('K*100.0 equals ' + str(K2))
    return None
    #return cmyk_object
    # The RGB numbers are in the range 0..255.
    # Change the RGB numbers to the range 0..1 by dividing them by 255.0.
    #return None  # Stub


def cmyk_to_rgb(cmyk):
    """
    Returns : color CMYK in space RGB.
    
    Formulae from en.wikipedia.org/wiki/CMYK_color_model.
   
    Parameter cmyk: the color to convert to a RGB object
    Precondition: cmyk is an CMYK object.
    """
    # The CMYK numbers are in the range 0.0..100.0.  Deal with them in the 
    # same way as the RGB numbers in rgb_to_cmyk()
    return None  # Stub


def rgb_to_hsv(rgb):
    """
    Return: color rgb in HSV color space.
    
    Formulae from wikipedia.org/wiki/HSV_color_space.
   
    Parameter rgb: the color to convert to a HSV object
    Precondition: rgb is an RGB object
    """
    # The RGB numbers are in the range 0..255.
    # Change them to range 0..1 by dividing them by 255.0.
    return None  # Stub


def hsv_to_rgb(hsv):
    """
    Returns: color in RGB color space.
    
    Formulae from http://en.wikipedia.org/wiki/HSV_color_space.
    
    Parameter hsv: the color to convert to a RGB object
    Precondition: hsv is an HSV object.
    """
    return None  # Stub
