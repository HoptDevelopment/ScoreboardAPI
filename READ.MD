### INSTRUCTIONS ###

#### Main Class ####
```
public void onEnable() {
    new ScoreboardUpdateUtil().runTaskTimerAsynchronously(this, 2, 2);
		
		for(Player p : Bukkit.getServer().getOnlinePlayers()) {
			PlayerBoard.get(p).setProvider(ScoreboardTimerProvider.getInstance());
		}
}

	public void onDisable()
	{
		instance = null; // for the skids
		try {
			PlayerBoard.dispose();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
```

#### Player Listeners ####
```
public class PlayerListener implements Listener
{
	
	@EventHandler
	public void onJoin(PlayerJoinEvent e) {
		PlayerBoard.get(e.getPlayer()).setProvider(ScoreboardTimerProvider.getInstance());
	}

	@EventHandler
	public void onQuit(PlayerQuitEvent e) {
		PlayerBoard.dispose(e.getPlayer());
	}
}
```

#### ScoreboardHandler ####
```
public class ScoreboardTimerProvider implements ScoreboardProvider
{

	public static ScoreboardTimerProvider instance;
	
	public ScoreboardTimerProvider() {
		instance = this;
	}
	
	@Override
	public String getTitle(Player player)
	{
		return ChatColor.translateAlternateColorCodes('&', "&6&lScoreboardExample");
	}

	@Override
	public String getHeader()
	{
		return ChatColor.translateAlternateColorCodes('&', "&7&m-------------------");
	}

	@Override
	public String getFooter()
	{
		return ChatColor.translateAlternateColorCodes('&', "&7&m-------------------");
	}

	@Override
	public List<String> getLinesFor(Player player)
	{
		List<String> arrays = new ArrayList<String>();
		
		arrays.add(ChatColor.translateAlternateColorCodes('&', "&6ScoreboardAPI Example"));
		
		return arrays;
	}
	
	public static ScoreboardTimerProvider getInstance() {
		return instance;
	}
}
```
