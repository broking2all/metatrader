#property indicator_chart_window
#property indicator_buffers 6
#property indicator_color1 DeepSkyBlue
#property indicator_color2 Red
#property indicator_color3 DeepSkyBlue
#property indicator_color4 Red
#property indicator_color5 DeepSkyBlue
#property indicator_color6 Red

 int Length = 11;
 extern double Slip = 1.8;
 int Risk = 1;
 int Signal = 1;
 int Line = 1;
 int Nbars = 1000;
double G_ibuf_100[];
double G_ibuf_104[];
double G_ibuf_108[];
double G_ibuf_112[];
double G_ibuf_116[];
double G_ibuf_120[];
 bool SoundON = FALSE;
bool Gi_128 = FALSE;
bool Gi_132 = FALSE;

// E37F0136AA3FFAF149B351F6A4C948E9
int init() {
   SetIndexBuffer(0, G_ibuf_100);
   SetIndexBuffer(1, G_ibuf_104);
   SetIndexBuffer(2, G_ibuf_108);
   SetIndexBuffer(3, G_ibuf_112);
   SetIndexBuffer(4, G_ibuf_116);
   SetIndexBuffer(5, G_ibuf_120);
   SetIndexStyle(0, DRAW_ARROW, STYLE_SOLID, 0);
   SetIndexStyle(1, DRAW_ARROW, STYLE_SOLID, 0);
   SetIndexStyle(2, DRAW_ARROW, STYLE_SOLID, 1);
   SetIndexStyle(3, DRAW_ARROW, STYLE_SOLID, 1);
   SetIndexStyle(4, DRAW_LINE);
   SetIndexStyle(5, DRAW_LINE);
   SetIndexArrow(0, 159);
   SetIndexArrow(1, 159);
   SetIndexArrow(2, 233);
   SetIndexArrow(3, 234);
   IndicatorDigits(MarketInfo(Symbol(), MODE_DIGITS));
   string Ls_0 = "BBands Stop(" + Length + "," + Slip + ")";
   IndicatorShortName(Ls_0);
   SetIndexLabel(0, "UpTrend Stop");
   SetIndexLabel(1, "DownTrend Stop");
   SetIndexLabel(2, "UpTrend Signal");
   SetIndexLabel(3, "DownTrend Signal");
   SetIndexLabel(4, "UpTrend Line");
   SetIndexLabel(5, "DownTrend Line");
   SetIndexDrawBegin(0, Length);
   SetIndexDrawBegin(1, Length);
   SetIndexDrawBegin(2, Length);
   SetIndexDrawBegin(3, Length);
   SetIndexDrawBegin(4, Length);
   SetIndexDrawBegin(5, Length);
   return (0);
}

// EA2B2676C28C0DB26D39331A336C6B92
int start() {
   int Li_0;
   double Lda_4[7000];
   double Lda_8[7000];
   double Lda_12[25000];
   double Lda_16[25000];
   for (int shift_20 = Nbars; shift_20 >= 0; shift_20--) {
      G_ibuf_100[shift_20] = 0;
      G_ibuf_104[shift_20] = 0;
      G_ibuf_108[shift_20] = 0;
      G_ibuf_112[shift_20] = 0;
      G_ibuf_116[shift_20] = EMPTY_VALUE;
      G_ibuf_120[shift_20] = EMPTY_VALUE;
   }
   for (shift_20 = Nbars - Length - 1; shift_20 >= 0; shift_20--) {
      Lda_4[shift_20] = iBands(NULL, 0, Length, Slip, 0, PRICE_CLOSE, MODE_UPPER, shift_20);
      Lda_8[shift_20] = iBands(NULL, 0, Length, Slip, 0, PRICE_CLOSE, MODE_LOWER, shift_20);
      if (Close[shift_20] > Lda_4[shift_20 + 1]) Li_0 = 1;
      if (Close[shift_20] < Lda_8[shift_20 + 1]) Li_0 = -1;
      if (Li_0 > 0 && Lda_8[shift_20] < Lda_8[shift_20 + 1]) Lda_8[shift_20] = Lda_8[shift_20 + 1];
      if (Li_0 < 0 && Lda_4[shift_20] > Lda_4[shift_20 + 1]) Lda_4[shift_20] = Lda_4[shift_20 + 1];
      Lda_12[shift_20] = Lda_4[shift_20] + (Risk - 1) / 2.0 * (Lda_4[shift_20] - Lda_8[shift_20]);
      Lda_16[shift_20] = Lda_8[shift_20] - (Risk - 1) / 2.0 * (Lda_4[shift_20] - Lda_8[shift_20]);
      if (Li_0 > 0 && Lda_16[shift_20] < Lda_16[shift_20 + 1]) Lda_16[shift_20] = Lda_16[shift_20 + 1];
      if (Li_0 < 0 && Lda_12[shift_20] > Lda_12[shift_20 + 1]) Lda_12[shift_20] = Lda_12[shift_20 + 1];
      if (Li_0 > 0) {
         if (Signal > 0 && G_ibuf_100[shift_20 + 1] == -1.0) {
            G_ibuf_108[shift_20] = Lda_16[shift_20];
            G_ibuf_100[shift_20] = Lda_16[shift_20];
            if (Line > 0) G_ibuf_116[shift_20] = Lda_16[shift_20];
            if (SoundON == TRUE && shift_20 == 0 && (!Gi_128)) {
               //Alert("BBA Alert Buy      ", Symbol(), "TF", Period());
               Gi_128 = TRUE;
               Gi_132 = FALSE;
            }
         } else {
            G_ibuf_100[shift_20] = Lda_16[shift_20];
            if (Line > 0) G_ibuf_116[shift_20] = Lda_16[shift_20];
            G_ibuf_108[shift_20] = -1;
         }
         if (Signal == 2) G_ibuf_100[shift_20] = 0;
         G_ibuf_112[shift_20] = -1;
         G_ibuf_104[shift_20] = -1.0;
         G_ibuf_120[shift_20] = EMPTY_VALUE;
      }
      if (Li_0 < 0) {
         if (Signal > 0 && G_ibuf_104[shift_20 + 1] == -1.0) {
            G_ibuf_112[shift_20] = Lda_12[shift_20];
            G_ibuf_104[shift_20] = Lda_12[shift_20];
            if (Line > 0) G_ibuf_120[shift_20] = Lda_12[shift_20];
            if (SoundON == TRUE && shift_20 == 0 && (!Gi_132)) {
               //Alert("BBA Alert Sell      ", Symbol(), "TF", Period());
               Gi_132 = TRUE;
               Gi_128 = FALSE;
            }
         } else {
            G_ibuf_104[shift_20] = Lda_12[shift_20];
            if (Line > 0) G_ibuf_120[shift_20] = Lda_12[shift_20];
            G_ibuf_112[shift_20] = -1;
         }
         if (Signal == 2) G_ibuf_104[shift_20] = 0;
         G_ibuf_108[shift_20] = -1;
         G_ibuf_100[shift_20] = -1.0;
         G_ibuf_116[shift_20] = EMPTY_VALUE;
      }
   }
   return (0);
}
