# Tello-drone
from djitellopy import Tello
import cv2, math, time

tello = Tello()
tello.connect()

tello.streamon()
frame_read = tello.get_frame_read()

tello.takeoff()

while True:
    # In ,reality you want to display frames in a separate thread. Otherwise,
    #  they will freeze while the drone moves.

    img = frame_read.frame
    cv2.imshow("drone", img)

    key = cv2.waitKey(1) & 0xff
    if key == 27:  # ESC
        break
    elif key == ord('w'):
        tello.move_forward(100)
    elif key == ord('s'):
        tello.move_back(100)
    elif key == ord('a'):
        tello.move_left(100)
    elif key == ord('d'):
        tello.move_right(100)
    elif key == ord('e'):
        tello.rotate_clockwise(100)
    elif key == ord('q'):
        tello.rotate_counter_clockwise(100)
    elif key == ord('r'):
        tello.move_up(100)
    elif key == ord('f'):
        tello.move_down(100)

tello.land()
