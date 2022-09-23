from telnetlib import STATUS
import Map

class node:

    def __init__(self):
        node.pos=[]
        node.g=0 #cost of getting to this node
        node.h=0 #estimated cost to goal
        node.f=0 #estimated total path: g+h
        node.child=[]
        node.parent=[]
    

def generate_successors(current_node,map_task):
    nextmove=[[current_node.pos[0],current_node.pos[1]-1],[current_node.pos[0],
    current_node.pos[1]+1],[current_node.pos[0]-1,current_node.pos[1],[current_node.pos[0]+1,current_node.pos[1]]]]
    
    allowed=[]
    for nextmove in nextmove:
        if map_task.get_cell_value(nextmove)>=0:
            allowed.append(nextmove)
    return allowed


def has_been_created(node,list_a,list_b):
    for el in list_a:
        if node.pos==el.pos:
            return el
    for el in list_b:
        if node.pos==el.pos:
            return el
    return node


def calculate_h(node,goal):
        return abs(node.pos[0]-goal[0])+abs(node.pos[1]-goal[1]) 

def attach_and_eval(node,parent,map_task):
    node.parent=parent
    node.g=parent.g+map_task.get_cell_value(node.pos)
    node.h=calculate_h(node,map_task.get_end_goal_pos())
    node.f=node.g+node.h

def propagate_path_improvments(P,map_task):
    for C in P.child:
        if P.g+map_task.get_cell_value(C.pos) < C.g:
            C.parent= P
            attach_and_eval(C,P,map_task)
            propagate_path_improvments(C, map_task)




def best_first_search(map_task):
    closed=[]
    open=[]
    x=node()
    x.pos=map_task.get_start_pos()
    open.append(x)
    while(x.pos != map_task.get_goal_pos()):
        if (len(open)==0):
            return("Failed")
        x=open.pop()
        closed.append(x)
        if (x.pos==map_task.get_goal_pos()):
            return("Succeed")
        SUCC=generate_successors(x,map_task)
        for S in SUCC:
            S_star=has_been_created(S,open,closed)
            x.child.append(S_star)
            if (S_star not in open and S_star not in closed):
                attach_and_eval(S_star,x,map_task)
                open.append(S_star)
                open.sort(key=lambda y: y.node.f,reverse=True)
            elif x.g + map_task.get_cell_value(S_star) < S_star.g:
                attach_and_eval(S_star,x,map_task)
                if S_star in closed:
                    propagate_path_improvments(S_star,map_task)

   


map_task=Map.Map_Obj(1)

best_first_search(map_task)
