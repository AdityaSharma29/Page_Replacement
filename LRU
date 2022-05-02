//                      PAGE REPLACEMENT   ---   LRU

#include <iostream>
#include <bits/stdc++.h>
#include <vector>
#include <utility>

using namespace std;

static int highest_number = 0;

int replace ( std::vector< pair <int, int>> *frames, int no_frames, std::vector<int> *track, int req) {
    
    int pf_flag = 0;
    pair < int, int> pr;
    
    std::vector<int>::iterator it = std::find( track->begin(), track->end(), req);
    // if page already present
    if (it != track->end()) {
        
        // update priority of the requested page in frames
        highest_number++;
        for (int i = 0; i < no_frames; i++) {
            if(frames->at(i).first == req ) { 
                frames->at(i).second = highest_number; 
                break; 
            }
        }
        return 0;
    }
    
    // page not present in main memory
    highest_number++;
    pf_flag = 1;
    
    // if empty frame found
    if( frames->size() < no_frames ){
        frames->push_back(make_pair( req, highest_number));
        track->push_back(req);
        return pf_flag;
    }
    
    // find the page to be replaced
    int minimun_priority = INT_MAX;
    int index = -1; 
    for (int i = 0; i < no_frames; i++) {
        if(frames->at(i).second < minimun_priority ) { index = i; minimun_priority = frames->at(i).second; }
    }
    
    // replace page in frames + track, update priority 
    frames->at(index).first = req;
    frames->at(index).second = highest_number;
    track->at(index) = req;
    
    return pf_flag;
}

int main() {
    
    int x, f;
    std::vector<int> req_seq;
    std::vector<int> track;
    vector < pair <int, int>> frames;
    pair < int, int> pr;
    
    // get no of frames 
    std::cout << " frames : ";
    std::cin >> f;

    // get the request sequence
    std::cout << "enter seq (-1 to end) : ";
    while(std::cin >> x){
        if(x==-1) break;
        req_seq.push_back(x);
    }
    
    // page fault count
    int pf_count = 0;   
    
    //traverse through request sequence
    for (int i = 0; i < req_seq.size(); i++) {
        pf_count += replace ( &frames, f, &track, req_seq[i]); 
    }
    
    std::cout << "pf_count : " << pf_count  << std::endl;
    
    for (int i=0; i<frames.size(); i++){
        cout << frames[i].first << " " << frames[i].second << endl;
    }
    
    return 0;
}
