# FragmentCross
How i pass data by fragment A -> Fragment B with EventBus
--click button FragmentA

Fragment B

  @Override
    public View onCreateView(
            @NonNull LayoutInflater inflater, ViewGroup container,
            Bundle savedInstanceState) {
       -->   EventBus.getDefault().register(this);
         root = inflater.inflate(R.layout.fragment_main, container, false);
        textView = root.findViewById(R.id.section_label);
        textView.setText(String.valueOf(index));

        return root;
    }
    
     @Override
    public void onDestroyView() {
        super.onDestroyView();
  -->      EventBus.getDefault().unregister(this);
    }
    
      //i receive event data
 -->   @Subscribe
    public void eventoRicevuto( MioEvento event){
        textView.setText(event.getData());
    }
    
    FragmentA
    // i send data
    public void sendDataBus(){
        // qui invio il dato
        EventBus.getDefault().post(new MioEvento("dati evento"));
    }
    
    // MY Class data
    
    public class MioEvento{
    public String getData() {
        return data;
    }

    String data;
    public MioEvento(String data){
        this.data=data;
    }
}
    
    
    
    
