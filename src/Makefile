DLIB=../extern/
DEPIC=$(DLIB)EpicFlow/
DRIC=$(DLIB)Ric-master/

DOPENCV=/usr/local/include/

LAPACKCFLAGS=#-DTHREADEDLAPACK
LAPACKLDFLAGS=-L/usr/lib64/atlas/ -llapack

CFLAGS=-DFINTEGER=int -fPIC -Wall -g -O3 -msse4 $(LAPACKCFLAGS) # -fopenmp -DUSE_OPENMP
LDFLAGS=-fPIC -Wall -g -O3 -msse4 -ljpeg -lpng $(LAPACKLDFLAGS)  #-fopenmp 

all: flowsac batch

flowsac: main.o impl.o flowsac.o segmentation.o utils.o epicInterpolation.o
	g++ $(DEPIC)image.o $(DEPIC)epic_aux.o $(DEPIC)variational.o $(DEPIC)variational_aux.o $(DEPIC)solver.o $(DEPIC)io.o -o $@ $^  $(shell pkg-config --libs opencv) $(LDFLAGS)   
	
batch: batch.o impl.o flowsac.o segmentation.o utils.o epicInterpolation.o callEpicFlow.o
	g++ $(DEPIC)image.o $(DEPIC)epic_aux.o $(DEPIC)variational.o $(DEPIC)variational_aux.o $(DEPIC)solver.o $(DEPIC)io.o $(DEPIC)epic.o $(DRIC)callRicflow.o $(DRIC)RIC.O $(DRIC)SLIC.o -o $@ $^  $(shell pkg-config --libs opencv) $(LDFLAGS) 
	
%.o:./%.cpp
	g++ -c $< -I$(DLIB) -I$(DLIB)/cvf/ -I$(DEPIC) -I$(DOPENCV) -w -fpermissive -std=c++11 $(CFLAGS) 

clean:
	rm main.o impl.o flowsac.o segmentation.o utils.o epicInterpolation.o batch.o callEpicFlow.o
