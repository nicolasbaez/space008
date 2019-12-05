## : : s p a c e 0 0 8

![space](https://github.com/nicolasbaez/space008/blob/master/space008.gif)

```processing
int cantidad=8192;
int maxVx=2;
float dCaida=0.1;
float dDist=4;
float orilla;
float distancia;
float nivel;
float caida=1;
float gotaXX[]=new float[cantidad];
float gotaYY[]=new float[cantidad];
float gotaZZ[]=new float[cantidad];
float gotaVx[]=new float[cantidad];
float gotaCaida[]=new float[cantidad];
float gotaDistancia[]=new float[cantidad];
float xx=0;
float yy=0;
float zz=0;
int cuadro=0;
void setup() {
  size(512, 256, P3D);
  orilla=0;
  distancia=width*0.1;
  nivel=0;
  for (int i=0; i<cantidad; i++) {
    gotaXX[i]=-width/2;
    gotaYY[i]=nivel;
    gotaZZ[i]=i;
    gotaVx[i]=random(maxVx)+1;
    gotaCaida[i]=orilla;
    gotaDistancia[i]=distancia;
  }
}
void draw() {
  translate(width/2, height/2, -height/2);
  rotateX(radians(xx));
  rotateY(radians(yy));
  rotateZ(radians(zz));
  background(0);
  for (int i=0; i<cantidad; i++) {
    if (gotaXX[i]>gotaCaida[i]) {
      gotaYY[i]=map(sin(radians(map(gotaXX[i], gotaCaida[i], gotaDistancia[i], 90, 180))), 1, 0, nivel, height*caida);
    }
    stroke(random(255), 255, 255);
    strokeWeight(1.5);
    point(gotaXX[i], gotaYY[i], gotaZZ[i]);
    if (gotaYY[i]<height*caida) {
      gotaXX[i]+=gotaVx[i];
    } else {
      gotaXX[i]=-width/2;
      gotaYY[i]=nivel;
      gotaVx[i]=random(maxVx)+1;
    }
  }
  xx=330;
  yy=200;
  zz=0;
  cuadro++;
  println(cuadro);
  if (cuadro>256&&cuadro<=1024) {
    saveFrame("gif/space008-######.png");
  }
}
```
