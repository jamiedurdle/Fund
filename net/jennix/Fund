package net.jennix;

import com.vk2gpz.tokenenchant.api.EnchantInfo;
import com.vk2gpz.tokenenchant.api.PotionHandler;
import com.vk2gpz.tokenenchant.api.TokenEnchantAPI;
import java.util.Random;
import org.bukkit.Bukkit;
import org.bukkit.command.Command;
import org.bukkit.command.CommandSender;
import org.bukkit.event.EventHandler;
import org.bukkit.event.EventPriority;
import org.bukkit.event.block.BlockBreakEvent;

public class Fund extends PotionHandler {
  private String path;
  
  public Fund(TokenEnchantAPI api) throws Exception {
    super(api);
    this.path = "Potions." + getName();
    loadConfig();
  }
  
  public boolean onCommand(CommandSender sender, Command command, String label, String[] args) {
    return true;
  }
  
  public String getName() {
    return "Fund";
  }
  
  public String getVersion() {
    return "1.0.0";
  }
  
  public Double getChange(int level) {
    return Double.valueOf(getConfig().getDouble(this.path + ".levels." + level));
  }
  
  public Double random() {
    Random randon = new Random();
    return Double.valueOf(randon.nextDouble() * 100.0D);
  }
  
  @EventHandler(priority = EventPriority.HIGHEST, ignoreCancelled = true)
  public void blockBreak(BlockBreakEvent e) {
    EnchantInfo ei = hasPotionEffect(e.getPlayer(), e.getPlayer().getItemInHand());
    if (ei == null || !canExecute(ei) || !checkCooldown(e.getPlayer()) || !isValid(e.getBlock().getLocation()))
      return; 
    if (getChange(ei.getLevel()).doubleValue() > random().doubleValue())
      Bukkit.dispatchCommand((CommandSender)Bukkit.getConsoleSender(), getConfig().getString(this.path + ".command").replaceAll("%player%", e.getPlayer().getName())); 
  }
}
